# SCUM ServerSettings Puppets Guide
File are in `ServerSettings.ini`

## การจำกัดจำนวน
| ชื่อการตั้งค่า | คำอธิบาย | Value |
|---|---|---|
| MaxAllowedCharacters | จำนวนตัวละครทั้งหมด(รวมผู้เล่น) | -1(Default) - 1024 |
| MaxAllowedZombies | จำนวน Puppet ทั้งหมด | 0 - 500 | 

## นิสัยผี
| ชื่อการตั้งค่า | คำอธิบาย | Value |
|---|---|---|
| EncounterCanRemoveLowPriorityCharacters | ? (ลบตัวละครไม่สำคัญอัตโนมัติ) | 0 - 1 |
| EncounterCanClampCharacterNumWhenOutOfResources | ? (ผีสามารถเกินจำนวนได้ถ้า Resource ไม่พอ) | 0 - 1 |
| PuppetsCanOpenDoors | ผีทุบเปิดประตูได้ | 0 - 1 |
| PuppetsCanVaultWindows | ผีกระโดดหน้าต่างได้ | 0 - 1 |
| DisableSuicidePuppetSpawning | ผีระเบิดเกิดได้ | 0 - 1 |

## ผีเกิดทั่วไป
### ตัวคูณจำนวนผี
โดย PerPlayer จะไม่นับกับผู้เล่นคนเดียว (Setting ชุดนี้ต้อง Re-Server)
| ชื่อการตั้งค่า | คำอธิบาย | Value |
|---|---|---|
| EncounterBaseCharacterAmountMultiplier | เกิดเมื่อผู้เล่นเข้าพื้นที่ | 0.0 - 10.0 |
| EncounterExtraCharacterPerPlayerMultiplier | เพิ่มตามผู้เล่นในพื้นที่ | 0.0 - 10.0 | 
| EncounterExtraCharacterPlayerCapMultiplier | ขีดจำกัดการเกิดตามผู้เล่นในพื้นที่ | 0.0 - 10.0 | 
| EncounterTotalCharactersSpawnedMultiplier  | คูณ จำนวนการเกิดทั้งหมด | 0.0 - 10.0 | 
| EncounterCharacterRespawnBatchSizeMultiplier | ? (คาดว่าเพิ่มขนาด ของกลุ่มเกิด) | 0.0 - 10.0 | 

### ลักษณะการเกิดผี
| ชื่อการตั้งค่า | คำอธิบาย | Value |
|---|---|---|
| EncounterCharacterRespawnTimeMultiplier | เวลาในการเกิด (ทีละตัว) 1.0 = 100 วิ | 0.0 - 100.0 |
| EncounterCharacterAggressiveSpawnChanceOverride | %ผีวิ่งมาหาเมื่อเกิด (ทะลุชุดกันผี) | -1.0*(Default) - 100.0 | 
| EncounterCharacterAINoiseResponseRadiusMultiplier | ระยะผีได้ยินเสียง Horde | 0 - 100.0 | 


## ผีขโยง HORDE
จะเกิดต่อเมื่อมีผีในพื้นที่ 1 ตัวขึ้นไป โดยจะเรียกผีรอบข้างเข้ามา พร้อมกับชุดผีที่เกิดเรื่อยๆ 
### ตัวคูณจำนวนผี
โดย PerPlayer จะไม่นับกับผู้เล่นคนเดียว (Setting ชุดนี้ต้อง Re-Server)
| ชื่อการตั้งค่า | คำอธิบาย | Value |
|---|---|---|
| EncounterHordeGroupBaseCharacterAmountMultiplier | จำนวนกลุ่ม Horde | 0.0 - 10.0 |
| EncounterHordeGroupExtraCharacterPerPlayerMultiplier | เพิ่มจำนวนกลุ่ม Horde ตามผู้เล่นในพื้นที่ | 0.0 - 10.0 | 
| EncounterHordeGroupExtraCharacterPlayerCapMultiplier | ขีดจำกัดการเกิดจำนวนกลุ่มHordeตามผู้เล่นในพื้นที่ | 0.0 - 10.0 | 
| EncounterHordeBaseCharacterAmountMultiplier | จำนวน Horde พื้นฐาน | 0.0 - 10.0 |
| EncounterHordeExtraCharacterPerPlayerMultiplier | เพิ่มจำนวน Horde ตามผู้เล่นในพื้นที่ | 0.0 - 10.0 | 
| EncounterHordeExtraCharacterPlayerCapMultiplier | ขีดจำกัดการเกิดจำนวน Horde ตามผู้เล่นในพื้นที่ | 0.0 - 10.0 | 

### ลักษณะการเกิดผี
| ชื่อการตั้งค่า | คำอธิบาย | Value |
|---|---|---|
| EncounterHordeActivationChanceMultiplier | ตัวคูณ % เกิด Horde | 0.0 - 10000.0 |
| EncounterHordeNoiseCheckCooldownMultiplier | ? (คูลดาวน์เกิด Horde) | -1.0*(Default) - 10000.0 | 
| EncounterHordeSpawnDistanceMultiplier | ระยะเกิดผี Horde | 0 - 100.0 | 
| EncounterHordeGroupRefillTimeMultiplier | ? (เวลาเติมกลุ่มผี) | 0 - 100.0 | 
