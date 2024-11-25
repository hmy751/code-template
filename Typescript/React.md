# ReactNode, ReactElement, JSX.Element, Element 타입 차이

- ReactElement는 리액트의 요소를 나타내는 가장 기본 구성단위로 JSX 또는 createElement를 호출하여 생성된 객체를 나타낸다.
- JSX.Element는 JSX표현식이 컴파일된 결과물을 나타내는 타입으로 결국 반환값이 ReactElement를 나타내게 된다.
- ReactNode는 포괄적인 타입으로 ReactElement를 포함하여 리액트가 렌더링할 수 있는 모든갑을 의미하며 string등도 포함된다.
- Element는 브라우저의 DOM요소를 나타낸다.

```ts
type ReactNode =
  | ReactChild
  | ReactFragment
  | ReactPortal
  | boolean
  | null
  | undefined;
```

# 합성형 패턴

```ts
import { ReactNode, ReactElement } from "react";
import styles from "./Dialog.module.css";
import * as D from "@radix-ui/react-dialog";

interface DialogProps {
  children: ReactNode;
}

function Dialog({ children }: DialogProps): ReactElement {
  return <D.Root>{children}</D.Root>;
}

Dialog.Content = ({ children }: { children: ReactNode }) => (
  <D.Portal>
    <D.Overlay />
    <D.Content className="content">{children}</D.Content>
  </D.Portal>
);
Dialog.Trigger = ({ children }: { children: ReactNode }) => (
  <D.Trigger>{children}</D.Trigger>
);
Dialog.Title = ({ children }: { children: ReactNode }) => (
  <D.Title className="title">{children}</D.Title>
);
Dialog.Description = ({ children }: { children: ReactNode }) => (
  <D.Description className="description">{children}</D.Description>
);

interface DialogType {
  Trigger: typeof Dialog.Trigger;
  Content: typeof Dialog.Content;
  Title: typeof Dialog.Title;
  Description: typeof Dialog.Description;
}

const TypedDialog = Dialog as typeof Dialog & DialogType;

export default TypedDialog;
```
