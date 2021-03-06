---
id: onAfterKeystroke
title: On After Keystroke
---

| Code | Can be called by                                                                                                                                                                                                                                                           | Definition                                                                                                                                     |
| ---- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| 28   | [4D Write Pro area](FormObjects/writeProArea_overview) - [Combo Box](FormObjects/comboBox_overview.md) - Form - [Input](FormObjects/input_overview.md) - [List Box](FormObjects/listbox_overview.md) - [List Box Column](FormObjects/listbox_overview.md#list-box-columns) | A character is about to be entered in the object that has the focus. `Get edited text` returns the object's text **including** this character. |


## 説明

> The `On After Keystroke` event can generally be replaced by the [`On After Edit`](onAfterEdit.md) event (see below).

After the [`On Before Keystroke`](onBeforeKeystroke.md) and `On After Keystroke` event properties are selected for an object, you can detect and handle the keystrokes within the object, using the `FORM event` command that will return `On Before Keystroke` and then `On After Keystroke` (for more information, please refer to the description of the `Get edited text` command).

These events are also activated by language commands that simulate a user action like `POST KEY`.

Keep in mind that user modifications that are not carried out using the keyboard (paste, drag-drop, etc.) are not taken into account. To process these events, you must use [`On After Edit`](onAfterEdit.md).

> The [`On Before Keystroke`](onBeforeKeystroke.md) and `On After Keystroke` events are not generated when using an input method. An input method (or IME, Input Method Editor) is a program or a system component that can be used to enter complex characters or symbols (for example, Japanese or Chinese) using a Western keyboard.

### 参照
[On Before Keystroke](onBeforeKeystroke.md).