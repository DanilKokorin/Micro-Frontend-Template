### Чтобы запустить корневой проект 

1. `npm install`
2. `npm start`

### Версия Node.js на которой я запускал проект  

> 20.17.0

====

# Как это всё работает
  
## Запуск микрофронтов 

В файле `src/index.ejs` есть фрагмент кода с уже подключенными микрофронтами, как он выглядит: 

```html
   <script type="systemjs-importmap">
     {
       "imports": {
         "@micro-frontend-app/root-config": "//localhost:10000/micro-frontend-app-root-config.js",
         "@micro-frontend-app/react": "//localhost:9080/micro-frontend-app-react.js",
         "@micro-frontend-app/vue": "https://production-server.com/micro-frontend-app-vue.js"
       }
     }
   </script>
```
***Это пример***


Тут есть **3** микрофронта, которые уже подлючены 

1. **root-config** - Это наш корневой проект, который мы только что запустили, он и собирает все микрофронты 
2. **react** - Это проект на react.js, мы его запустили отдельно. Чтобы это сделать, нужно прям зайти в проект и запустить его как отдельный фронтенд проект
3. **vue** - Это проект на vue.js, чтобы получить его мы обращаемся на сервер, его лежит его сборка (то есть делать с ним ничего не надо) 

***Например, если мы хотим, чтобы все наши фронты были на сервере, надо поменять значение ключа, в котором лежит микрофронт***

## Как добавить новый микрофронт 

1. Добавить его в файл `src/index.ejs` в скрипт: 

```html
    <script type="systemjs-importmap">
     {
       "imports": {
         "@micro-frontend-app/root-config": "//localhost:10000/micro-frontend-app-root-config.js",
         "@micro-frontend-app/react": "//localhost:9080/micro-frontend-app-react.js",
         "@micro-frontend-app/vue": "https://production-server.com/micro-frontend-app-vue.js"

         "@micro-frontend-app/vue2": "//localhost:9090/micro-frontend-app-vue2.js",
       }
     }
   </script>
```

2. Добавить новый роутер в файл `microfrontend-layout`, например: 

```html
    <route path="vue2">
      <application name="@micro-frontend-app/vue2"></application>
    </route>
```