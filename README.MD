# Лекция 2
## Что изменилось/добавилось:

### Изменения в HTML:

   1. Добавлен элемент интерфейса пользователя: В новой версии добавлен элемент <div> с идентификатором user-interface, внутри которого размещено изображение кнопки перезапуска игры.
   2. Добавлено изображение кнопки перезапуска: В новой версии добавлен тег <img> с идентификатором restart-btn для отображения изображения кнопки перезапуска игры.

   ```html
<!-- Добавлен элемент интерфейса пользователя -->
<div id="user-interface">
    <img id="restart-btn" src="assets/restart.png" />
</div>
```

### Изменения в CSS:

   1. Обновлены стили: В новой версии добавлены стили для элемента интерфейса пользователя (#user-interface) и изображения кнопки перезапуска (#restart-btn), чтобы обеспечить их корректное отображение.

```css
<!-- Добавлен элемент интерфейса пользователя -->
#user-interface {
    margin: 0;
    width: 100%;
    height: 100vh;
}

#restart-btn {
    position: absolute;
    right: 0;
    bottom: 0;
    width: 100px;
}
``` 

### Изменения в JavaScript:

   1. Изменена начальная позиция камеры: В новой версии изменена начальная позиция камеры, чтобы улучшить видимость сцены.
   2. Добавлен генератор теней: В новой версии добавлен генератор теней shadowGenerator для создания и рендеринга теней от объектов на сцене.
   3. Добавлены объекты платформы и мяча: В новой версии добавлены объекты платформы (platform) и мяча (ball) для создания игрового мира.
   4. Использование текстур: В новой версии добавлено использование текстур для материалов объектов платформы и мяча.
   5. Добавлены тени для мяча: В новой версии добавлены тени для мяча с помощью shadowGenerator.
   6. Улучшены эффекты теней: В новой версии улучшены эффекты теней с помощью использования размытия и настройки параметров теней.

```javascript
// Добавление генератора теней
var shadowGenerator = new BABYLON.ShadowGenerator(1024, light);

// Создание платформы
let platform = new BABYLON.MeshBuilder.CreateBox('box', {
    width: 6,
    height: 0.1,
    depth: 6,
    wrap: true
}, scene);
let boxMaterial = new BABYLON.StandardMaterial("material", scene);
boxMaterial.emissiveTexture = new BABYLON.Texture('assets/platform.png');
platform.material = boxMaterial;
platform.receiveShadows = true;

// Создание мяча
let ball = new BABYLON.MeshBuilder.CreateSphere("sphere", { diametr: 1 }, scene);
ball.position = new BABYLON.Vector3(0, 0.5, 0);
let ballMaterial = new BABYLON.StandardMaterial("material", scene);
ballMaterial.emissiveTexture = new BABYLON.Texture('assets/ball.png');
ball.material = ballMaterial;
shadowGenerator.getShadowMap().renderList.push(ball);

// Работа с тенями
shadowGenerator.useBlurExponentialShadowMap = true;
shadowGenerator.useKernelBlur = true;
shadowGenerator.blurKernel = 64;
```