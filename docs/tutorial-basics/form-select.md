---
sidebar_position: 3
---

# Form Select

Form select are used for single value select lists or multiple value select lists, they have search embeded inside them, and these are built to work with react-hook-form.

To configure this component you first need to install chakra-react-select package, to do that run this command in your favourite CLI while being in your project directory.

```shell
npm install chakra-react-select
```

or

```shell
yarn add chakra-react-select
```


Here is a global component for this.

```jsx
import React from "react";
import { Select } from "chakra-react-select";
import {
  Flex,
  FormControl,
  FormErrorMessage,
  FormLabel,
  Icon,
  IconButton,
  chakra,
  useColorMode,
} from "@chakra-ui/react";
import { Controller } from "react-hook-form";
import { getColor, colorKeys } from "../../../config/constants/appColors";
import APP_ICONS from "../../../config/constants/icons";

const FormSearchSelect = ({
  label,
  placeholder,
  options = [],
  errors,
  id,
  control,
  required = false,
  rules,
  multiple,
  containerStyles,
  onRefresh,
  inputProps,
}) => {
  const { colorMode } = useColorMode();
  if (required) {
    required = `${label} is required`;
  }
  return (
    <Controller
      control={control}
      name={id}
      rules={{
        required: required,
        ...rules,
      }}
      render={({ field: { onChange, onBlur, value, ref, ...rest } }) => (
        <Flex align="end" w="full">
          <FormControl isInvalid={errors[id]} {...containerStyles}>
            <FormLabel htmlFor={id} fontSize={"13px"}>
              {label}
              {required && (
                <chakra.span color={getColor(colorKeys.danger, colorMode)}>
                  *
                </chakra.span>
              )}
            </FormLabel>

            <Select
              allowClear={true}
              isMulti={multiple}
              onChange={(e) => {
                if (multiple) {
                  onChange({
                    target: {
                      name: id,
                      value: e.map((item) => item.value),
                    },
                  });
                } else {
                  onChange({
                    target: {
                      name: id,
                      value: e.value,
                    },
                  });
                }
              }}
              value={
                multiple
                  ? options?.filter((option) => value?.includes(option.value))
                  : options?.filter(function (option) {
                      return option.value === value;
                    })
              }
              ref={ref}
              placeholder={placeholder}
              options={options}
              {...rest}
              leftAddon={
                <chakra.span
                  fontSize="1.2em"
                  color={getColor(colorKeys.primary, colorMode)}
                  mr="0.5em"
                >
                  {APP_ICONS.SEARCH}
                </chakra.span>
              }
              {...inputProps}
            ></Select>
            <FormErrorMessage>
              {errors[id] && errors[id].message}
            </FormErrorMessage>
          </FormControl>
          {onRefresh && (
            <IconButton
              onClick={onRefresh}
              ml="1em"
              aria-label="Search database"
              icon={<Icon boxSize={7} as={APP_ICONS.REFRESH} />}
            />
          )}
        </Flex>
      )}
    />
  );
};

export default FormSearchSelect;
```

It can be used like this

```jsx
<FormSearchSelect
  id="language"
  label="Language"
  placeholder={"Select Language"}
  required={true}
  errors={errors}
  control={control}
  options={[
    {
      label: "English",
      value: "English",
    },
    {
      label: "Urdu",
      value: "Urdu",
    },
  ]}
  inputProps={{ size: "sm" }}
/>
```
