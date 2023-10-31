---
layout: page
title: UnityTools
subtitle: Useful tools I've made on Unity Engine
cover-img: "/assets/projects/unity-tools/cover.png"
---

## Preview Generator
PreviewGenerator is a tool that generate Sprite images of Prefabs  
Just select some Prefabs & Right Click > Create > Sprite Preview  

| [![screenshot preview](https://github.com/Tequiloutre/UnityTools/blob/main/Screenshots/Screen_Preview.png?raw=true)](https://github.com/Tequiloutre/UnityTools/blob/main/Screenshots/Screen_Preview.png?raw=true) | [![screenshot sprite](https://github.com/Tequiloutre/UnityTools/blob/main/Screenshots/Screen_Preview_Sprite.png?raw=true)](https://github.com/Tequiloutre/UnityTools/blob/main/Screenshots/Screen_Preview_Sprite.png?raw=true) |

[📥Download Package](https://github.com/Tequiloutre/UnityTools/releases/download/preview-generator_v2/PreviewGenerator_v2.unitypackage)  
[📥Source code](https://github.com/Tequiloutre/UnityTools/tree/main/UnityTools/Assets/Scripts/PreviewGenerator)

<hr>

## EditCondition
EditCondition is a CustomAttribute used to show or hide fields depending on another value  
ex : The field "value" is only showed when the bool field "condition" is true

```cs
[SerializeField] private bool condition = false;
[SerializeField, EditCondition("condition")] private int value = 0;
```

| [![screenshot condition false](https://github.com/Tequiloutre/UnityTools/blob/main/Screenshots/Screen_EditCondition_False.png?raw=true)](https://github.com/Tequiloutre/UnityTools/blob/main/Screenshots/Screen_EditCondition_False.png?raw=true) | [![screenshot condition true](https://github.com/Tequiloutre/UnityTools/blob/main/Screenshots/Screen_EditCondition_True.png?raw=true)](https://github.com/Tequiloutre/UnityTools/blob/main/Screenshots/Screen_EditCondition_True.png?raw=true) |

[📥Download Package](https://github.com/Tequiloutre/UnityTools/releases/download/v1/Unity_EditCondition.unitypackage)  
[📥Source code](https://github.com/Tequiloutre/UnityTools/tree/main/UnityTools/Assets/Scripts/EditCondition)

<hr>

## SerializableDictionary
SDictionary is a Class working as a classic C# Dictionary but it can be serialized and edited in Inspector

```cs
[SerializeField] private SDictionary<string, int> dico = new SDictionary<string, int>();
```

| [![screenshot dictionary](https://github.com/Tequiloutre/UnityTools/blob/main/Screenshots/Screen_Dico.png?raw=true)](https://github.com/Tequiloutre/UnityTools/blob/main/Screenshots/Screen_Dico.png?raw=true) |

[📥Download Package](https://github.com/Tequiloutre/UnityTools/releases/download/v2/SerializableDictionary_v2.unitypackage)  
[📥Source code](https://github.com/Tequiloutre/UnityTools/tree/main/UnityTools/Assets/Scripts/SerializableDictionary)
