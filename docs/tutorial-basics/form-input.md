---
sidebar_position: 2
---

# Form Input

Form inputs are used for textual, number etc type input fields, and these are built to work with react-hook-form, here is a global component for this.

```jsx
import {
  FormControl,
  chakra,
  FormErrorMessage,
  FormLabel,
  Icon,
  Input,
  InputGroup,
  InputRightElement,
  useColorMode,
} from "@chakra-ui/react";
import React from "react";
import { Controller } from "react-hook-form";
import APP_ICONS from "../../../config/constants/icons";
import { getColor, colorKeys } from "../../../config/constants/appColors";

const FormInput = ({
  label,
  placeholder,
  id,
  required = false,
  errors = {},
  control,
  rules,
  containerStyles,
  type,
  leftAddon,
  rightAddon,
  inputProps,
  hideLabel,
  secure,
}) => {
  const [show, setShow] = React.useState(false);
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
        <FormControl isInvalid={errors[id]} {...containerStyles}>
          {!hideLabel && (
            <FormLabel htmlFor={id} fontSize={"13px"}>
              {label}
              {required && (
                <chakra.span color={getColor(colorKeys.danger, colorMode)}>
                  *
                </chakra.span>
              )}
            </FormLabel>
          )}
          <InputGroup>
            {leftAddon}
            <Input
              value={value}
              onChange={onChange}
              onBlur={onBlur}
              ref={ref}
              placeholder={placeholder}
              id={id}
              type={secure ? (show ? "text" : "password") : type}
              {...inputProps}
              {...rest}
            />
            {secure ? (
              <InputRightElement h="full">
                <Icon
                  as={show ? APP_ICONS.EYE : APP_ICONS.EYE_OFF}
                  boxSize={5}
                  onClick={() => setShow(!show)}
                />
              </InputRightElement>
            ) : (
              <InputRightElement
                display={errors[id] ? "flex" : "none"}
                h="full"
              >
                <Icon
                  as={APP_ICONS.WARNING}
                  color={getColor(colorKeys.danger, colorMode)}
                  boxSize={5}
                />
              </InputRightElement>
            )}
            {rightAddon}
          </InputGroup>
          <FormErrorMessage>
            {errors[id] && errors[id].message}
          </FormErrorMessage>
        </FormControl>
      )}
    />
  );
};

export default FormInput;
```

It can be used like this

```jsx
<FormInput
  label={"Driver Share (%)"}
  type={"number"}
  control={control}
  errors={errors}
  id="driverShare"
  required={true}
  placeholder="Enter Percentage"
  inputProps={{ size: "sm" }}
/>
```
