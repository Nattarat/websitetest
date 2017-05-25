# SASS

## SASS syntax

* String
```
$prefix-binding: 'bind';
```

* String containing quote
```
$warning: "You can\'t do that.";
$warning: 'You can\'t do that.';
```

* Value
```
$font-primary: Prompt;
$screen-mobile-xs: 320px;
```

* List value
```
$font-stack: ('Helvetica', 'Arial', sans-serif);
```

* Url
```
.foo {
  background-image: url('../images/logo.svg');
}
```

* Calculation
```
.foo {
  width: (100% / 3);
}
```

## Variable name
* สร้างชื่อแบบใช้ - ในการขั้นระหว่างคำ
* ใช้ SASS maps ร่วมกับ Variables เพื่อความเป็นระเบียบในการเรียกใช้งาน (จุดประสงค์เพื่อการจัดหมวดหมู่ Variable)
```
$url-image
$abbreviation-mobile
$screen-mobile-xs-max
```

## Class name
### Component
```
.name-extendedName {...}
```
โครงสร้างชื่อ ประกอบด้วย
1. name: ชื่อที่ตั้งขึ้นต้องสอดคล้องกับหน้าตา/หน้าที่ของ Component
2. extendedName: ชื่อประเภทของ Component ใช้เพื่อขยายความหมายของหน้าตาและหน้าที่
3. ชื่อประกอบด้วยคำ 2 คำ ขั้นด้วยขีดกลาง และถ้าคำๆ นั้นมีคำขยายหลายคำให้เขี่ยนต่อกันโดยใช้ตัวเล็ก เช่น
    * .card-primary {...}
    * .container-verticalmiddle {...}

### Child element in component
```
.componentName-extendedName {...}
```
โครงสร้างชื่อ ประกอบด้วย
1. componentName: ชื่อของ Component (ไม่รวม extendedName)
2. extendedName: ชื่อของ Element ใน Component ใช้เพื่อขยายความหมายของหน้าตาและหน้าที่
3. ชื่อประกอบด้วยคำ 2 คำ ขั้นด้วยขีดกลาง และถ้าชื่อของ Element ใน Component มีคำขยายหลายคำให้เขี่ยนต่อกันโดยใช้ตัวเล็ก เช่น
    * .card-wrappermeta {...}
    * .card-title {...}
    * .container-inner {...}

```
ตัวอย่าง
.card-primary {
  .card-wrapperouter {...}
  .card-wrapperinner {...}
  .card-wrapperbutton {...}
  .card-wrappermeta {
    .card-image {...}
    .card-title {...}
    .card-description {...}
  }
}

.container-verticalmiddle {
  > .container-inner {...}
}
```

### State & Modifier class of component
```
.name-extendedName {
  &.prefixName-stateName {...}
  &.prefixName-modifierName {...}
}
```
โครงสร้างชื่อ ประกอบด้วย
1. prefixName: คำนำหน้าเพื่อระบุว่าใช้ใน Scope ของ Component นี้เท่านั้น เช่น bind, state, uniq เป็นต้น
2. stateName/modifierName: ชื่อ State/Modifier ของ Component ใช้เพื่อระบุว่าอยู่ในสถานะอะไร หรือใช้กับสิ่งใด
3. ชื่อประกอบด้วยคำ 2 คำ ขั้นด้วยขีดกลาง และถ้าชื่อของ State/Modifier มีหลายคำให้เขี่ยนต่อกันโดยใช้ตัวเล็ก เช่น
    * &.state-disable {...}
    * &.bind-stripe {...}
    * &.bind-bannerhero {...}
    * &.bind-backgroundcover {...}

```
ตัวอย่าง
.message-notification {
  &.state-disable {...}
  &.state-pendingforevaluation {...}
  &.state-successall {...}

  &.bind-formal {...}
  &.bind-positiontopright {...}
  &.bind-sizelarge {...}
  &.bind-contentinner {...}
}
```

## CSS ruleset
* แบ่งส่วนประกอบเป็น 6 ส่วน ได้แก่
  1. Specific variables(use only in component)
  2. Styles of component itself
  3. Styles of child class
  4. Styles of state
  5. Styles of state with modifier class
  6. Media query
* เขียน Nesting ซ้อนไม่เกิน 3 ชั้น(แต่ในงานจริงๆ เราจะเจอการใช้ Selector ที่มีการซ้อนมากกว่า 3 ชั้น ก็จะอนุโลมให้ในกรณี Class นั้นซ้อนอยู่ใน State, Modifier class, Media query)
* Media query เพื่อความยืดหยุ่นจะเขียนที่ Component class ไม่เขียนที่ Mixin เพราะ Component class อาจจะมีรูปแบบ Child class เพิ่มเติมจากใน Mixin และมีช่วง Media query ที่แตกต่างกัน

```
.component {
  // SPECIFIC VARIABLES(USE ONLY IN COMPONENT)
  // >>>>>>>>>>>>>>>>>>>>>>>
  $use-for-purpose: 1px;

  // MIXINS
  // >>>>>>>>>>>>>>>>>>>>>>>
  @include ellipsis;
  @include size($length);

  // STYLES OF COMPONENT ITSELF
  // >>>>>>>>>>>>>>>>>>>>>>>
  display: block;
  overflow: hidden;
  margin: 0 auto;

  // STYLES OF CHILD CLASS
  // >>>>>>>>>>>>>>>>>>>>>>>
  .component-child {
    text-transform: uppercase;

    .component-child-inner {
      content: 'Inner';
    }

    // *** If not needed, shouldn't use inline class for create style ***
    // .component-child-inner .component-child-inner-deep {
    //   content: 'Deep inner';
    // }

    .component-child-inner-deep {
      content: 'Deep inner';
    }
  }

  // STYLES OF STATE
  // >>>>>>>>>>>>>>>>>>>>>>>
  &:hover {
    color: red;
  }

  &.state-disabled {
    color: gray;
  }

  // STYLES OF STATE WITH MODIFIER CLASS
  // >>>>>>>>>>>>>>>>>>>>>>>
  // - overwrite style of component itself, states and child classes)
  // - "binding" prefix is used for reuse modifier
  // - "uniq" prefix is used for specific modifier (instead id selector)
  &.binding-component-modifier {
    // Styles of component itself

    // Styles of state
    &:hover {
      color: blue;
    }

    &.state-disabled {
      color: white;
    }

    // Styles of child class
    .component-child {
      text-transform: capitalize;

      // *** if component child is wrapped by state or modifier class or media query >>> allow more than 3 level nesting >>> to remain class structure ***
      .component-child-inner {
        content: 'Binding modifier - inner';
      }

      .component-child-inner-deep {
        content: 'Binding modifier - deep inner';
      }
    }
  }

  &.uniq-component-modifier {
    // Styles of component itself

    // Styles of state
    &:hover {
      color: green;
    }

    &.state-disabled {
      color: yellow;
    }

    // Styles of child class
    .component-child {
      text-transform: lowercase;

      // *** if component child is wrapped by state or modifier class or media query >>> allow more than 3 level nesting >>> to remain class structure ***
      .component-child-inner {
        content: 'Uniq modifier - inner';
      }

      .component-child-inner-deep {
        content: 'Uniq modifier - deep inner';
      }
    }
  }

  // MEDIA QUERY
  // >>>>>>>>>>>>>>>>>>>>>>>
  // MEDIA QUERY: Styles of component itself
  @include mq($from: screens(mobile-xs)) {
    // Styles of component itself
  }

  // MEDIA QUERY: Styles of state
  &:hover {
    @include mq($from: screens(mobile-xs)) {
      // Styles of component itself
      color: orange;

      // Styles of child class
    }
  }

  &.state-disabled {
    @include mq($from: screens(mobile-xs)) {
      // Styles of component itself
      color: black;

      // Styles of child class
    }
  }

  // MEDIA QUERY: Styles of child class
  .component-child {
    @include mq($from: screens(mobile-xs)) {
      text-transform: uppercase;

      // Styles of child class
      // *** if component child is wrapped by state or modifier class or media query >>> allow more than 3 level nesting >>> to remain class structure ***
      .component-child-inner {
        content: 'MEDIA QUERY: Styles of child class - inner';
      }

      .component-child-inner-deep {
        content: 'MEDIA QUERY: Styles of child class - deep inner';
      }
    }
  }

  // MEDIA QUERY: Styles of state with modifier class
  &.binding-component-modifier {
    // Styles of component itself

    // Styles of state
    &:hover {
      @include mq($from: screens(mobile-xs)) {
        // Styles of component itself
        color: purple;

        // Styles of child class
      }
    }

    &.state-disabled {
      @include mq($from: screens(mobile-xs)) {
        // Styles of component itself
        color: skyblue;

        // Styles of child class
      }
    }

    // Styles of child class
    .component-child {
      @include mq($from: screens(mobile-xs)) {
        text-transform: none;

        // Styles of child class
        // *** if component child is wrapped by state or modifier class or media query >>> allow more than 3 level nesting >>> to remain class structure ***
        .component-child-inner {
          content: 'MEDIA QUERY: Styles of state with modifier class - inner';
        }

        .component-child-inner-deep {
          content: 'MEDIA QUERY: Styles of state with modifier class - deep inner';
        }
      }
    }
  }

  &.uniq-component-modifier {
    // Styles of component itself

    // Styles of state
    &:hover {
      @include mq($from: screens(mobile-xs)) {
        // Styles of component itself
        color: magenta;

        // Styles of child class
      }
    }

    &.state-disabled {
      @include mq($from: screens(mobile-xs)) {
        // Styles of component itself
        color: maroon;

        // Styles of child class
      }
    }

    // Styles of child class
    .component-child {
      @include mq($from: screens(mobile-xs)) {
        text-transform: none;

        // Styles of child class
        // *** if component child is wrapped by state or modifier class or media query >>> allow more than 3 level nesting >>> to remain class structure ***
        .component-child-inner {
          content: 'MEDIA QUERY: Styles of state with modifier class - inner';
        }

        .component-child-inner-deep {
          content: 'MEDIA QUERY: Styles of state with modifier class - deep inner';
        }
      }
    }
  }
}
```

## Note
1. การสร้าง Variable ใหม่ มีแนวทางดังนี้
    * Value มีการใช้ซ้ำ
    * Value มีการเปลี่ยนแปลงในอนาคต
2. Magic number
    * ตัวเลขที่มีความเฉพาะเจาะจง เกิดขึ้นมาโดยไม่มีความเกี่ยวข้องกับใคร ใช้ในการแก้ไขปัญหาเฉพาะหน้าเท่านั้น
    * ต้องเขียน Comment กำกับไว้เสมอว่าใช้เพื่ออะไร และเมื่อปัญหาผ่านไปแล้วต้องกลับมาคิดแก้ไขเลขตัวนี้
3. การทำ Formatting and syntax เพื่อสร้างรูปแบบที่สามารถนำมาวิเคราะห์ข้อดี-ข้อเสีย และไว้ใช้อ้างอิงการแก้ไขในอนาคตได้
4. ข้อดีของ nest 3 ชั้น คือ เวลากด Ctrl + k + 2 or 3 or 4 เพื่อ Folding code แล้วเราจะอ่านโค้ดได้ง่าย และไล่ได้เร็ว
5. Media query เขียนใน Scope ของแต่ละ Class ถึงจะเยอะ แต่ไล่จัดการได้ง่าย
