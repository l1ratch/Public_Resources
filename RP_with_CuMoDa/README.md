Чтобы собрать ресурспак с кастомной текстурой, использующей `CustomModelData`, выполните следующие шаги:

### 1. **Структура папок ресурспака**
Создайте папки в соответствии со структурой Minecraft. Пример для предмета `iron_sword`:
```
resourcespack/
├── pack.mcmeta
└── assets/
    └── minecraft/
        ├── models/
        │   └── item/
        │       └── iron_sword.json
        └── textures/
            └── item/
                └── custom_sword.png
```

### 2. **Настройка pack.mcmeta**
Добавьте файл `pack.mcmeta` в корень ресурспака:
```json
{
  "pack": {
    "pack_format": 15, // Укажите версию, совместимую с вашей версией Minecraft
    "description": "Ресурспак с кастомной текстурой"
  }
}
```

### 3. **Создание модели предмета**
В файле `assets/minecraft/models/item/iron_sword.json` укажите кастомную модель через `overrides`:
```json
{
  "parent": "item/handheld",
  "textures": {
    "layer0": "item/iron_sword"
  },
  "overrides": [
    {
      "predicate": {
        "custom_model_data": 12345 // Ваш идентификатор
      },
      "model": "item/custom_sword"
    }
  ]
}
```

### 4. **Модель для кастомной текстуры**
Создайте `assets/minecraft/models/item/custom_sword.json`:
```json
{
  "parent": "item/handheld",
  "textures": {
    "layer0": "item/custom_sword"
  }
}
```

### 5. **Добавление текстуры**
Поместите вашу текстуру в `assets/minecraft/textures/item/custom_sword.png`.

### 6. **Проверка в игре**
Используйте команду для выдачи предмета с `CustomModelData`:
```minecraft
/give @p iron_sword{CustomModelData:12345} 1
```

### Важные нюансы:
- **Версия pack_format**: Убедитесь, что значение в `pack.mcmeta` соответствует версии игры (например, 15 для 1.20.4).
- **Тип предмета**: Кастомная модель должна наследоваться от существующего предмета (в примере — `iron_sword`).
- **Текстуры**: Поддерживайте разрешение, кратное 16 (например, 16x16, 32x32).
- **Отладка**: Используйте F3 + T для перезагрузки ресурспаков в игре.

### Пример для нескольких текстур:
Если нужно добавить несколько текстур, расширьте список `overrides`:
```json
"overrides": [
  {
    "predicate": { "custom_model_data": 12345 },
    "model": "item/custom_sword"
  },
  {
    "predicate": { "custom_model_data": 67890 },
    "model": "item/another_sword"
  }
]
```

Готовый ресурспак можно запаковать в ZIP-архив и поместить в папку `resourcepacks` игры.