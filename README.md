# Client Instalation
  
## Устанавливаем react

```bash
mkdir client
cd client
create-react-app ./
```

## Настраиваю webpack config (опционально)
 
    По умолчанию разработчики не могут настраивать Webpack или Babel, пока не сделают eject.
    Для этого сбрасываю git и делаю eject. Внимание eject нельзя отменить!!!

 ```bash
git reset --hard
yarn eject
```   
    В появившейся папке config в файле webpack.config.js
    добавляю константу - путь к алиасам ( ну например на том же уровне что и файл)

```js
const aliases = require('./aliases');
```
   создаю соответственно файл aliases.js подключаю переменную path
```js
const path = require('path');
```
   и далее указываю все нужные алиасы к директориам (например) 
```js
module.exports = {
  styles: path.join(__dirname, '../src/styles'),
  components: path.join(__dirname, '../src/components'),
  utils: path.join(__dirname, '../src/utils'),
  assets: path.join(__dirname, '../src/assets'),
  ...
}
```   
  и добавляю переменную aliases в файле webpack.config.js moduleFileExtensions

```js
    alias: {
        // Support React Native Web
        // https://www.smashingmagazine.com/2016/08/a-glimpse-into-the-future-with-react-native-for-web/
        'react-native': 'react-native-web',
        ...aliases,
        // Allows for better profiling with ReactDevTools
        ...(isEnvProductionProfile && {
          'react-dom$': 'react-dom/profiling',
          'scheduler/tracing': 'scheduler/tracing-profiling',
        }),
        ...(modules.webpackAliases || {}),
      },
```

   теперь мне эти директории станут доступны внутри проэкта по простому пути (например)
```js
import { Component_name } from 'components';
//or
import  Component_name  from 'components';
```
```scss
@import '~styles/variables';
```

## Устанавливаем зависимости
```js
yarn add react-router react-router-dom socket.io-client react-scroll-to-bottom react-emoji query-string
```




# Server Instalation
  
  
## Устанавливаем nodejs

```bash
mkdir server
cd server
npm init -y
```

## Устанавливаем зависимости
```js
npm install --save cors nodemon express socket.io
```

Абсолютно у всех разработчиков знакомство с nodejs начинается с того, что после каждого изменения нужно перезагружать сервер. Поэтому мы разберем, как сделать так, чтобы сервер перегружался автоматически.

Самый популярный вариант - это nodemon. То есть идея состоит в том, что в development окружении мы хотим, чтобы nodemon следил за файлами, которые мы меняем и просто перезапускал сервер, если эти файлы относятся к серверу.

## Добавляем nodemon start to package.json

```json
 "scripts": {
    "start": "nodemon index.js",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
```