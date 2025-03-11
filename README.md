# Angular Intro

Angular Tutorial online: https://angular.dev/tutorials/first-app
## Angular CLI (https://angular.dev/tools/cli/setup-local)
### Instaliavimas
```bash
npm install -g @angular/cli
ng new <pavadinimas>
#arba
npx -p @angular/cli ng new <pavadinimas>
```

Angular CLI yra pagrindinis komandinės eilutės "pagalbininkas", leidžiantis efektyviai dirbti su Angular. CLI naudojamas visoms Angular komandoms leisti, bei visiems komponentams ir kitiems failams generuoti. Naudojant CLI, niekada nereikėtų kurti failo nuo nulio - visada galima jį tiesiog sugeneruoti, ir framework pats sukuria reikalingus failus bei bazinę kodo struktūra juose.

`ng new <pavadinimas>` sukuria naują Angular projektą. Komanda taip pat užduoda pagrindinius klausimus projekto konfigūracijai, tokius kaip norimas CSS preprocesorius (kaip SCSS).

### Angular Schematics (https://angular.dev/cli/generate)

Angular CLI turi generatoriaus funkcionalumą per komandą `ng generate`. Jo pagalba, kursime skirtingų tipų resursus, kaip komponentus: `ng generate <tipas> <pavadinimas>`.
```bash
- ng generate component tasks
- ng generate service task
- ng generate pipe upper
# Taip pat yra sutrumpintos versijos
- ng g c tasks
- ng g s task
- ng g p upper
```
## Angular projekto struktūra (https://angular.dev/reference/configs/workspace-config)

```bash
/angular.json - pagrindinis Angular projekto failas. Šiame faile 
/tsconfig.json - Typescript konfigūracija projekte.
/package.json - NPM paketo failas, aprašantis dependencies.
/public - statiniai failai, kaip paveikslėliai.
/src/index.html - pagrindinis index failas, kuriame galima rasti "root" Angular komponentą.
/src/main.ts - "pirminis" failas, kuriame inicializuojamas Angular.
/src/app - pagrindiniai kodo failai. Direktorija, kur "gyvena" visas Angular kodas.
```

## Angular Components (https://angular.dev/guide/components)

Komponentai - pagrindinis Angular statybinis elementas. Visos Angular aplikacijos, galiausiai, yra tiesiog įvairių komponentų mix'ai. Generuojami `ng generate component <name>`. Generatorius sugeneruos keturis failus:
1. `<name>.component.ts` - pagrindinis komponento Typescript failas.
2. `<name>.component.spec.ts` - Typescript test failas.
3. `<name>.component.scss` - komponento stilių failas. Šiuo atveju SCSS.
4. `<name>.component.html` - komponento HTML failas, kuriame parodoma komponento HTML struktūra.

### Komponento dekoratorius

Angular-specific elementus kode galima atskirti pagal `@Dekoratorius`. Komponentai aprašomi `@Component` dekoratoriumi:
```typescript
@Component({
  selector: 'app-root', //HTML tag'as, kuriuo komponentas pasiekiamas
  imports: [RouterOutlet], //komponento priklausomybės (dependencies)
  templateUrl: './app.component.html', //kelias iki komponento HTML failo
  styleUrl: './app.component.scss' //kelias iki komponento stilių failo
})
export class AppComponent {
  title = 'test';
}
```

Vietoje `templateUrl` galima naudoti `template`, kuris leidžia HTML rašyti tiesiai Typescript failo viduje. HTML rašomas tiesiogiai, kaip `template: '<div></div>'`. Taip pat ir su stiliais, vietoje `styleUrl` naudojant `style` - CSS rašome tiesiai kaip parametrą.

`imports` aprašo visas komponento priklausomybes, tokias kaip naudojamos direktyvos, pipe'ai arba kiti komponentai. Svarbu prisiminti, kad kitų komponentų arba direktyvų HTML kode negalima naudoti tol, kol jie nėra importuoti. Tai galioja ir jūsų parašytiems komponentams, ir standartiniams, pačiame Angular esantiems.

### Angular control flow (https://angular.dev/guide/templates/control-flow)

Komponento HTML kode galima vykdyti logiką, priklausomai nuo kintamųjų reikšmių. Tam Angular sukurti "control flow" pagalbiniai elementai. Jie rašomi tiesiai kode ir primena standartinius Javascript loginius operatorius:
- `@if`:
```html
@if (a > b) {
  {{a}} is greater than {{b}}
} @else if (b > a) {
  {{a}} is less than {{b}}
} @else {
  {{a}} is equal to {{b}}
}
```
- `@for`:
```html
@for (item of items; track item.id) {
  {{ item.name }}
}
```

## Direktyvos (https://angular.dev/guide/directives)

Direktyvas galima pavadinti "komponentais be HTML". Jos aprašomos labai panašiai kaip komponentai, tačiau užuot turinčios template, jos operuoja su kitu, komponente jau esančiu, HTML. Generuojamos `ng generate directive <name>`.


## Task #1
> Jūs esate jaunesnysis programuotojas startuolyje, kuriantis asmeninį užduočių sekiklį. Jūsų tikslas – sukurti Angular programėlę, kurioje vartotojai galėtų:
>
> 1.Pridėti naują užduotį į sąrašą.<br/>
> 2.Peržiūrėti užduočių sąrašą, atvaizduojamą dinamiškai.<br/>
> 3.Rodyti pranešimą, kai nėra jokių užduočių.

## Angular Pipes (https://angular.dev/guide/templates/pipes)

Angular Pipes leidžia vizualiai transformuoti HTML turinį, nekeičiant duomenų, kurie rodomi. Labai naudinga, norint suformatuoti, arba kitaip pakeisti rodomus duomenis.

Naudojamas Pipe pavadinimą rašant po stačiojo brūkšnio kintamojo interpoliacijoje - `{{ kintamasis | pipe}}`.

Galima sugeneruoti naują pipe naudojant `ng generate pipe <vardas>`, arba naudoti vieną iš egzistuojančių standartinių pipe, kaip `CurrencyPipe`, `DatePipe`, `UppercasePipe`, `LowercasePipe` ir kt.

## Task #2

> Startuolio CEO prisiskaitė knygų apie Silicon Valley ir jo kultūrą ir nusprendė, kad būtina optimizuoti darbuotojų laisvą nuo darbo laiką. Nauja užduotis - pridėti užduoties pridėjimo laiką prie kiekvienos pridedamos užduoties.
>
> 1. Pakeiskime užduotį iš teksto į objektą, kuris turi `text` ir `date` laukus.<br/>
> 2. `date` lauką užpildykit naudodami `Date` pagalbinį objektą. Jo turinys - mygtuko paspaudimo laikas.<br/>
> 3. `TaskComponent` viduje, naudokite `DatePipe` ir pavaizduokit kiekvienos užduoties laiką `shortTime` formatu. Kaip pridėti formatą - https://angular.dev/api/common/DatePipe#format-examples.<br/>
> 4. (Extra): sugeneruokite naują pipe, kuris, naudojant `toLocaleTimeString` su opcijomis, grąžintų Lietuvai ('lt-lt') lokalizuotą datą. Naudokite `{ weekday: "long", year: "numeric", month: "long", day: "numeric" }` kaip parametrus.
