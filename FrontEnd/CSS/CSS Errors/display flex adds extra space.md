---
keywords: |-
  flex-grow with display flex adds extra space
  flex-grow adds extra space
---
Does it add extra height?
- if so the you need to add `flex-direction: column`
Does it add extra width?
- if so the you need to add `flex-direction: row`
###### Why does this happen?
probably one of the child of the element with both flex grow and flex display property has a manual height property, manual height property is not considered by flex box, so what happens is on top of flex grow, it also adds the manual height making the overall height extra.