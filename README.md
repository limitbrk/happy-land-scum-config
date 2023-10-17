# SCUM Admin Settings

การตั้งค่าสำหรับ [HAPPY LAND PvE 100%](https://discord.gg/KwXqDWx4W4)

## SCUM Loot Modification

อ่านเพิ่มเติม [ที่นี่](https://github.com/limitbrk/happy-land-scum-config/tree/master/Loot/README.md)


## SCUM Trader Configuarator
File are in `EconomyOverride.json`
```json
{
  "economy-override": {
    "economy-reset-time-hours": "-1.0",
    "prices-randomization-time-hours": "-1.0",
    "tradeable-rotation-time-ingame-hours-min": "48.0",
    "tradeable-rotation-time-ingame-hours-max": "96.0",
    "tradeable-rotation-time-of-day-min": "8.0",
    "tradeable-rotation-time-of-day-max": "16.0",
    "fully-restock-tradeable-hours": "2.0",
    "trader-funds-change-rate-per-hour-multiplier": "1.0",
    "prices-subject-to-player-count": "1",
    "gold-price-subject-to-global-multiplier": "1",
    "economy-logging": "1",
    "traders-unlimited-funds": "0",
    "traders-unlimited-stock": "0",
    "only-after-player-sale-tradeable-availability-enabled": "1",
    "tradeable-rotation-enabled": "1",
    "enable-fame-point-requirement": "1",
    "traders": {
      "A_0_Armory": [
        {
          "tradeable-code": "Frag_Grenade",
          "base-purchase-price": "-1",
          "base-sell-price": "-1",
          "delta-price": "-1.0",
          "can-be-purchased": "default",
          "required-famepoints": "-1"
        }
      ],
      "A_0_BoatShop": [],
      "A_0_Hospital": [],
      "A_0_Mechanic": [],
      "A_0_Saloon": [],
      "A_0_Trader": [],
      "A_0_Barber": [],
      "B_4_Armory": [],
      "B_4_BoatShop": [],
      "B_4_Hospital": [],
      "B_4_Mechanic": [],
      "B_4_Saloon": [],
      "B_4_Trader": [],
      "B_4_Barber": [],
      "C_2_Armory": [],
      "C_2_BoatShop": [],
      "C_2_Hospital": [],
      "C_2_Mechanic": [],
      "C_2_Saloon": [],
      "C_2_Trader": [],
      "C_2_Barber": [],
      "Z_3_Armory": [],
      "Z_3_BoatShop": [],
      "Z_3_Hospital": [],
      "Z_3_Mechanic": [],
      "Z_3_Saloon": [],
      "Z_3_Trader": [],
      "Z_3_Barber": []
    }
  }
}
```
### Global
| ชื่อการตั้งค่า | คำอธิบาย | ค่าที่รองรับ |
|---|---|---|
| `economy-reset-time-hours` | เวลาชั่วโมงที่ใช้ในการ Set Fund = 0 และ Restock ของ ค่าน้อยกว่า 0 คือไม่กำหนด | ตัวเลขทศนิยม ค่าเริ่มต้น -1.0 |
| `prices-randomization-time-hours` | เวลาชั่วโมงที่ใช้ในการสุ่มราคาใหม่ ค่าน้อยกว่า 0 คือไม่กำหนด | ตัวเลขทศนิยม ค่าเริ่มต้น -1.0 |
| `fully-restock-tradeable-hours` | เวลาชั่วโมงที่ใช้ในการ Restock ของให้เต็ม ค่าน้อยกว่า 0 คือไม่กำหนด | ตัวเลขทศนิยม ค่าเริ่มต้น 2.0 |
| `trader-funds-change-rate-per-hour-multiplier` | ตัวคูณความเร็วในการ Refill เงิน ของ NPC 10000$/Hour | ตัวเลขทศนิยม ค่าเริ่มต้น 1.0 |
| `traders-unlimited-funds` | Fund ไม่จำกัด | 0 - ปิด 1 - เปิด |
| `traders-unlimited-stock` | Stock ไม่จำกัด | 0 - ปิด 1 - เปิด |
| `economy-logging` | เปิด Log ซื้อขาย NPC | 0 - ปิด 1 - เปิด |
| `prices-subject-to-player-count` | ปรับราคาอ้างอิงตามจำนวนผู้เล่นใน Server | 0 - ปิด 1 - เปิด |
| `tradeable-rotation-enabled` | เปิดการ Rotation ของ | 0 - ปิด 1 - เปิด |
| `tradeable-rotation-time-ingame-hours-min` | ระยะเวลาเล่นเกมเพื่อ Rotation ต่ำสุด | ตัวเลขทศนิยม ค่าเริ่มต้น 48.0 |
| `tradeable-rotation-time-ingame-hours-max` | ระยะเวลาเล่นเกมเพื่อ Rotation สูงสุด | ตัวเลขทศนิยม ค่าเริ่มต้น 96.0 |
| `tradeable-rotation-time-of-day-min` | ระบุเวลาสำหรับการ Rotation ต่ำสุด | ตัวเลขทศนิยม ค่าเริ่มต้น 8.0 |
| `tradeable-rotation-time-of-day-max` | ระบุเวลาสำหรับการ Rotation สูงสุด | ตัวเลขทศนิยม ค่าเริ่มต้น 16.0 |
| `gold-price-subject-to-global-multiplier` | เรทราคาซื้อทองผันผวนไป | ตัวเลขทศนิยม ค่าเริ่มต้น 1.0 |
| `only-after-player-sale-tradeable-availability-enabled` | จะมี Stock ใหม่เมื่อผู้เล่นขายของให้เท่านั้น | 0 - ปิด 1 - เปิด |
| `enable-fame-point-requirement` | เปิด ต้องการซื้อด้วย Famepoint | 0 - ปิด 1 - เปิด |

### Trader
จะระบุภายใต้ `traders`

| ชื่อการตั้งค่า | คำอธิบาย | ค่าที่รองรับ |
|---|---|---|
| `tradeable-code` | Item ที่ต้องการเปลี่ยนแปลงค่า | ตัวอักษร |
| `base-purchase-price` | ราคาซื้อNPC ค่าน้อยกว่า 0 คือราคาเริ่มต้น | ตัวเลข ค่าเริ่มต้น -1 (ถ้าเติม g ต่อท้าย จะใช้เป็น Gold) |
| `base-sell-price` | ราคาขายNPC ค่าน้อยกว่า 0 คืออัตราขายเริ่มต้น | ตัวเลข ค่าเริ่มต้น -1 (ไม่รองรับขายเป็น Gold) |
| `delta-price` | อัตราสุ่มราคาสินค้า ค่า 0 คือไม่สุ่ม ค่าน้อยกว่า 0 คืออัตราขายเริ่มต้น | ตัวเลขทศนิยม ค่าเริ่มต้น -1.0 |
| `can-be-purchased` | ตั้งสินค้าขาย | default - ตาม Dev true - ขาย false - ไม่ขาย |
| `required-famepoints` | FP ที่ต้องการเพื่อซื้อ ค่า 0 คือไม่ต้องการ ค่าน้อยกว่า 0 คือค่าเริ่มต้น | ตัวเลขทศนิยม ค่าเริ่มต้น -1.0 |

### FAQ
> Item ไหน ตั้งขายได้บ้าง
> ``` 
> ถ้า ขาย NPC มีแถบสีเหลืองติดราคา แสดงว่าตั้งขายได้
> ```