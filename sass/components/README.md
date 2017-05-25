# Components
---

## components folder
* มีหน้าที่เก็บไฟล์สไตล์ที่มีลักษณะเป็น widget สามารถนำไปใช้ในแต่ละส่วนของเว็บไซต์ได้(resue) โดยไม่มีความเฉพาะเจาะจงเท่ากับ layout
* อ้างอิง components จาก Semantic UI

## components structure
* Mixins: เป็นส่วนที่กำหนด properties, states, child classes รวมไปถึง sizes เพื่อทำให้เกิดโครงสร้างของ component
* Contextual variations: เป็นส่วนการตั้งค่าให้กับ variables ของ mixin เพื่อสร้าง component class ออกมาใช้งาน
* เขียน nesting ไม่เกิน 3 ชั้น(ถ้าเกิน 3 ชั้นให้เขียนแบบบรรทัดเดียวแทน)
* เขียน media query ที่ contextual variations แทนการเขียนที่ mixins(เพราะ ที่ component class นั้น อาจจะมีรูปแบบ child classes แตกต่างจาก mixins และอาจจะมีช่วง media query ไม่เหมือนกัน ดังนั้นการเขียน media query ที่ mixins จึงไม่ยืดหยุ่นพอ)