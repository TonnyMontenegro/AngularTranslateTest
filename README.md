
# TranlationTest

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 13.1.2.

## Development server

Run `ng serve` for a dev server. Navigate to `http://localhost:4200/`. The app will automatically reload if you change any of the source files.

## Code scaffolding

Run `ng generate component component-name` to generate a new component. You can also use `ng generate directive|pipe|service|class|guard|interface|enum|module`.

## Build

Run `ng build` to build the project. The build artifacts will be stored in the `dist/` directory.

## Running unit tests

Run `ng test` to execute the unit tests via [Karma](https://karma-runner.github.io).

## Running end-to-end tests

Run `ng e2e` to execute the end-to-end tests via a platform of your choice. To use this command, you need to first add a package that implements end-to-end testing capabilities.

## Further help

To get more help on the Angular CLI use `ng help` or go check out the [Angular CLI Overview and Command Reference](https://angular.io/cli) page.


## Explicacion rapida del funcionamiento e integracion con BabelEdit

se instala ngx translate

```bash
npm install @ngx-translate/core @ngx-translate/http-loader rxjs --save
```

Se importan los modulos 

`@ngx-translate/core`
`@ngx-translate/http-loader`

En **app.module.ts**

en imports debajo de BrowserModule

```typescript
 // ngx-translate and the loader module
        HttpClientModule,
        TranslateModule.forRoot({
            loader: {
                provide: TranslateLoader,
                useFactory: HttpLoaderFactory,
                deps: [HttpClient]
            }
        })
```

luego de nuestra clase **AppModule**

```typescript
// required for AOT compilation
export function HttpLoaderFactory(http: HttpClient): TranslateHttpLoader {
    return new TranslateHttpLoader(http);
}
```

---
en nuestro **app.component.ts**
importamos el modulo:
```typescript
import {TranslateService} from '@ngx-translate/core';
```
y dentro de la clase **AppComponent** creamos el constructor
```typescript
constructor(private translate: TranslateService) {
        translate.setDefaultLang('en');
    }
```

---
Colocamos nuestra traducciones en **assets/i18n/{{LANG}}.json**

---
en nuestros componentes HTML podemos emplear las traduccione sd ela siguiente manera
```html
<div>
    <h1>{{ 'welcome.title' | translate }}</h1>

    <!-- translation: translation pipe -->
    <p>{{ 'welcome.text' | translate }}</p>

    <!-- translation: directive (key as attribute)-->
    <p [translate]="'welcome.text'"></p>

    <!-- translation: directive (key as content of element) -->
    <p translate>welcome.text</p>
</div>
```

para realizar el cambio de lenguaje creamos una funcion en nuestro **app.component.ts**

```typescript
useLanguage(language: string): void {
    this.translate.use(language);
}
```
luego podemos instanciar un evento para el cambio de idioma
```html
<button (click)="useLanguage('en')">en</button>
```


---

De cara a **BabelEdit**, es muy simple solo se abren los json de traduccion y con una intefaz simple y opciones variadas de corrección podemos brindarle la herramienta a los traductores sin preocuparnos por que toquen código.
