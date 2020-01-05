---
title: Markdown
main_menu: true
---

## Heading levels
`#`의 개수에 따라 글씨 크기가 조절되고 기본적으로 굵은 글씨로 표현된다. 페이지 제목은 H1으로 렌더링 된다. H1-H6 순으로 크기가 작아진다.

### H3

This is in an H3 section.

#### H4

This is in an H4 section.

##### H5

This is in an H5 section.

###### H6

This is in an H6 section.

### Inline text styles

- **bold**
- _italic_
- ***bold italic***
- ~~strikethrough~~
- <u>underline</u>
- _<u>underline italic</u>_
- **<u>underline bold</u>**
- ***<u>underline bold italic</u>***
- `monospace text`
- **`monospace bold`**

```markdown
- **bold**
- _italic_
- ***bold italic***
- ~~strikethrough~~
- <u>underline</u>
- _<u>underline italic</u>_
- **<u>underline bold</u>**
- ***<u>underline bold italic</u>***
- `monospace text`
- **`monospace bold`**
```

### color text
[html color code](https://htmlcolorcodes.com/color-picker/)

{{<color value="red" text="중요">}}

```
{{</* color value="red" text="중요" */>}}
```

## Lists
하위 목록을 만들려면 두개의 탭(4칸)을 들여써야한다.

### 글머리 기호 리스트
`-` 혹은 `*`를 사용한다.
- This is a list item
* This is another list item in the same list
- 상위 목록
    - 하위 목록1
        - 하위 목록의 하위 목록
    - 하위 목록2
```
- This is a list item
* This is another list item in the same list
- 상위 목록
    - 하위 목록1
        - 하위 목록의 하위 목록
    - 하위 목록2
```

### 번호 리스트

1.  리스트 1
1. markdown에서 상요하는 숫자가 반드시 최종 출련의 숫자와 관련있지는 않는다.    
3.  {{<note>}}
      노트에도 번호 리스트를 사용할 수 있다.
    {{</note>}}

<!-- separate lists -->

1.  새로운 리스트. 새로운 리스트를 시작하려면 `<!-- separate lists -->`을 추가해야한다.
2.  목록 하위에 블록 요소가 포함될 수 있다.

      하위 블록

      ```bash
      ls -l
      ```

    - 하위 목록1

```
1.  리스트 1
1. markdown에서 상요하는 숫자가 반드시 최종 출련의 숫자와 관련있지는 않는다.    
3.  {{<note>}}
      노트에도 번호 리스트를 사용할 수 있다.
    {{</note>}}

<!-- separate lists -->

1.  새로운 리스트. 새로운 리스트를 시작하려면 `<!-- separate lists -->`을 추가해야한다.
2.  목록 하위에 블록 요소가 포함될 수 있다.

      하위 블록

      ```bash
      ls -l
      ```

    - 하위 목록1
```

### Tab
{{< tabs name="tab_lists_example" >}}
{{% tab name="Choose one..." %}}
Please select an option.
{{% /tab %}}
{{% tab name="Formatting tab lists" %}}

Tabs may also nest formatting styles.

1. Ordered
2. (Or unordered)
3. Lists

```bash
echo 'Tab lists may contain code blocks!'
```

{{% /tab %}}
{{% tab name="Nested headers" %}}

### Header within a tab list

Nested header tags may also be included.

{{< warning >}}
Headers within tab lists will not appear in the Table of Contents.
{{< /warning >}}

{{% /tab %}}
{{< /tabs >}}


### Checklists
- [ ] This is a checklist item
- [x] This is a selected checklist item

```
- [ ] This is a checklist item
- [x] This is a selected checklist item
```

### Code blocks
[코드블럭](https://gohugo.io/content-management/syntax-highlighting/#list-of-chroma-highlighting-languages)
```
this is a code block created by back-ticks
```

```markdown
    ```
    this is a code block created by back-ticks
    ```
```

## Links
### 외부 링크
[Link to Kubernetes.io](https://kubernetes.io/)

```
[Link to Kubernetes.io](https://kubernetes.io/)
```
### 내부 링크
[InnerLink](/)
```
[InnerLink]](/)
```

## Images
### In markdown

![kubernetes](/images/kubernetes-horizontal-color.png)
```
![kubernetes](/images/kubernetes-horizontal-color.png)
```
### In html(width 조절 가능)
{{<image src="/images/kubernetes-horizontal-color.png" width="400">}}

```
{{</* image src="/images/kubernetes-horizontal-color.png" width="400" */>}}
```

## Videos
### Youtube
{{< youtube w7Ft2ymGmfc >}}
```
  {{</* youtube w7Ft2ymGmfc */>}}
```
### Videos
{{<iframe src="/images/docs/Docker/chapter2/Summary.mp4">}}
```
{{</* iframe src="/images/docs/Docker/chapter2/Summary.mp4"*/>}}
```

## Tables

| Heading cell 1 | Heading cell 2 |
| -------------- | -------------- |
| Body cell 1    | Body cell 2    |

```
| Heading cell 1 | Heading cell 2 |
| -------------- | -------------- |
| Body cell 1    | Body cell 2    |
```

## Admonitions
{{< note >}}
Notes catch the reader's attention without a sense of urgency.

You can have multiple paragraphs and block-level elements inside an admonition.

| Or | a | table |
{{< /note >}}

{{< caution >}}
The reader should proceed with caution.
{{< /caution >}}


{{< warning >}}
Warnings point out something that could cause harm if ignored.
{{< /warning >}}

```
{{</* note */>}}
Notes catch the reader's attention without a sense of urgency.
You can have multiple paragraphs and block-level elements inside an admonition.
| Or | a | table |
{{</* /note */>}}
{{</* caution */>}}
The reader should proceed with caution.
{{</* /caution */>}}
{{</* warning */>}}
Warnings point out something that could cause harm if ignored.
{{</* /warning */>}}
```

## Katacoda Embedded Live Environment

{{< kat-button >}}

```
{{</* kat-button */>}}
```
