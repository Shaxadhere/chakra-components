---
sidebar_position: 1
---

# Form Container

Form containers will be used to containerized forms, all apps will render inside this component.

### Form Modal

If you are willing to use modal forms you can use this form container.

```jsx
import React from "react";
import {
  Button,
  Box,
  Modal,
  ModalOverlay,
  ModalCloseButton,
  ModalHeader,
  ModalBody,
  ModalFooter,
  ModalContent,
} from "@chakra-ui/react";
import FormButton from "../FormButton";

const FormModal = ({
  title,
  disclosure,
  size = "2xl",
  id = "modal-form",
  containerProps,
  children,
  isSubmitting,
  onSubmit,
  reset,
  maxW,
  hideFooter,
}) => {
  const { isOpen, onClose } = disclosure;

  return (
    <Modal size={size} isOpen={isOpen} onClose={onClose} isCentered>
      <ModalOverlay />
      <ModalContent
        maxW={maxW}
        maxH={{ base: "unset", md: "calc(100vh - 50px)" }}
        overflow={"auto"}
        {...containerProps}
        rounded="sm"
      >
        <Box as="form" onSubmit={onSubmit}>
          <ModalCloseButton />
          <ModalHeader>{title}</ModalHeader>

          <ModalBody>{children}</ModalBody>

          {!hideFooter && (
            <ModalFooter>
              <Button
                variant="outline"
                mr={3}
                onClick={() => {
                  onClose();
                  reset && reset();
                }}
              >
                Cancel
              </Button>
              <FormButton
                type="submit"
                form={id}
                colorScheme="blue"
                isLoading={isSubmitting}
                onClick={onSubmit}
              >
                Save
              </FormButton>
            </ModalFooter>
          )}
        </Box>
      </ModalContent>
    </Modal>
  );
};

export default FormModal;
```

It can be used like this

```jsx
<FormModal
  title={"Form Title"}
  disclosure={disclosure}
  isSubmitting={loadingState}
  onSubmit={handleSubmit}
  containerProps={{ maxW: "75rem" }}
>
  {/* Rest of your form */}
</FormModal>
```

### Form Drawer

If you are willing to use modal forms you can use this form container.

```jsx
import React from "react";
import {
  Button,
  Box,
  Modal,
  ModalOverlay,
  ModalCloseButton,
  ModalHeader,
  ModalBody,
  ModalFooter,
  ModalContent,
} from "@chakra-ui/react";
import FormButton from "../FormButton";

const FormDrawer = ({
  title,
  disclosure,
  size = "2xl",
  id = "modal-form",
  placement = "right",
  containerProps,
  children,
  isSubmitting,
  onSubmit,
  reset,
  maxW,
  hideFooter,
}) => {
  const { isOpen, onClose } = disclosure;

  return (
    <Drawer
      size={size}
      isOpen={isOpen}
      onClose={onClose}
      isCentered
      placement={placement}
    >
      <DrawerOverlay />
      <DrawerContent
        maxW={maxW}
        maxH={{ base: "unset", md: "calc(100vh - 50px)" }}
        overflow={"auto"}
        {...containerProps}
        rounded="sm"
      >
        <Box as="form" onSubmit={onSubmit}>
          <DrawerCloseButton />
          <DrawerHeader>{title}</DrawerHeader>

          <DrawerBody>{children}</DrawerBody>

          {!hideFooter && (
            <DrawerFooter>
              <Button
                variant="outline"
                mr={3}
                onClick={() => {
                  onClose();
                  reset && reset();
                }}
              >
                Cancel
              </Button>
              <FormButton
                type="submit"
                form={id}
                colorScheme="blue"
                isLoading={isSubmitting}
                onClick={onSubmit}
              >
                Save
              </FormButton>
            </DrawerFooter>
          )}
        </Box>
      </DrawerContent>
    </Drawer>
  );
};

export default FormModal;
```

It can be used like this

```jsx
<FormDrawer
  title={"Form Title"}
  disclosure={disclosure}
  isSubmitting={loadingState}
  onSubmit={handleSubmit}
  containerProps={{ maxW: "75rem" }}
  placement="left"
>
  {/* Rest of your form */}
</FormDrawer>
```
