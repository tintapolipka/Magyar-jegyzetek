## Utility Types: 
Beépített típusok, mint például Readonly, Partial, Required, amelyek segítenek bonyolultabb típusok létrehozásában és ellenőrzésében.
https://www.typescriptlang.org/docs/handbook/utility-types.html


Awaited: Ha Promise lenne a típus, ami majd visszatér valamilyen típussal, akkor a Promise
Awaited-be foglalásával rögtön a várható értéktípust kapjuk meg.
https://www.typescriptlang.org/docs/handbook/utility-types.html#awaitedtype
```typescript
type A = Awaited<Promise<string>>; //type A = string
```
Conditional Types: Olyan típusokat hozhatunk létre, amelyek egy feltételtől függnek, például ellenőrizhetjük, 
hogy egy típus egy másik típus altípusa-e.
https://www.typescriptlang.org/docs/handbook/2/conditional-types.html
```typescript
SomeType extends OtherType ? TrueType : FalseType;
// például:
interface MyDate extends Date {
    randiDate:string,
}
type RandiDate = MyDate extends Date? string : number; // string
```

Exclude: Létrehoz egy új típust, amely kizárja egy unió típusból azokat az elemeket, amelyek egy másik típusnak megfelelnek.
https://www.typescriptlang.org/docs/handbook/utility-types.html#excludeuniontype-excludedmembers
Formula: Exclude<UnionType, ExcludedMembers>
```typescript
  type T0 = Exclude<"a" | "b" | "c", "a">; //type T0 = "b" | "c"
  // Itt "a" | "b" | "c" únióból kizárjuk "a"-t
```

Indexed Access Types: Lehetővé teszi, hogy egy típus tulajdonságait kulcs alapján érjük el, hasonlóan ahhoz, ahogyan objektumok esetében történik.
https://www.typescriptlang.org/docs/handbook/2/indexed-access-types.html
```typescript
  type Person = { age: number; name: string; alive: boolean };
  // egy adott címkére kérdezve rá:
  type Age = Person["age"]; // type Age = number
  
  // egy únióra kérdezve rá:
  type I1 = Person["age" | "name"]; // type I1 = string | number
  
  // egy típus összes kulcsára a keyof-al kérdezve rá:
  type I2 = Person[keyof Person]; // type I2 = string | number | boolean
```

Infer: Használható feltételes típusokon belül, hogy egy típust kikövetkeztessen és későbbi felhasználásra elérhetővé tegyen.
https://www.typescriptlang.org/docs/handbook/2/conditional-types.html#inferring-within-conditional-types

///////////////// EZT MÉG NEM ÉRTEM! /////////////////////////

InstanceType: Egy osztály példányának típusát vonja ki.
https://www.typescriptlang.org/docs/handbook/utility-types.html#instancetypetype

# Mapped Types:
https://www.typescriptlang.org/docs/handbook/2/mapped-types.html
 Index signatures -t használva egy adott objektum minden key-ére 
 vonatkozva lehet valamit csinálni. A lenti példában a 'Property'
  a placeholder az adott key-nek, ami a Type-ban van. Itt az érték
 típusa a Type Property-edik elememének típusa, szóval az ami amúgy is lenne. 
 
```typescript
type MapTypes<Type> = {
  [Property in keyof Type]: Type[Property];
};
```
Arra használható jól, hogy readonly-vá tegyük, vagy levegyük azt minden key-value párról (-readonly leveszi, +readonly felteszi), így:
```typescript
type CreateMutable<Type> = {
  -readonly [Property in keyof Type]: Type[Property];
};
```
Az opcionalitását is meg lehet változtatni a key-nek (szintén - és + jellel). 
A lenti pédában kötelezővé teszi az eddig opcionális key-t így:



# NonNullable: Létrehoz egy új típust, amely kizárja a null és undefined értékeket a megadott típusból.
https://www.typescriptlang.org/docs/handbook/utility-types.html#nonnullabletype

Omit: Létrehoz egy új típust úgy, hogy eltávolítja egy meglévő típus néhány tulajdonságát.
https://www.typescriptlang.org/docs/handbook/utility-types.html#omittype-keys
```typescript
type SzukitetTipus = Omit<TeljesTipus,'egyik felesleges key'|'másik felesleges key'>
```
Figyelem! Ha később bővítem a TeljesTipus-t, akkor a SzukitetTipus-ba is bekerül
 az új key-value pár (Ha ezt nem akarom akkor Pick<>-et használjak)!

Partial: Egy objektumtípus összes tulajdonságát opcionálissá teszi.
https://www.typescriptlang.org/docs/handbook/utility-types.html#partialtype
```typescript
type MindenOpcionalis = Partial<TeljesTipus>;
// Így azonban minden key éréke lehet undefined is! 
// Ha akarok mégis kötelező mezőt:
type MajdnemMindenOpcionalis = Partial<TeljesTipus> & {egyikKey : string}; //egyikKey kötelező
```


Pick: Egy típust hoz létre úgy, hogy egy másik típusból csak a meghatározott tulajdonságokat választja ki.
https://www.typescriptlang.org/docs/handbook/utility-types.html#picktype-keys
```typescript
type KimazsolazottTipus = Pick<TeljesTipus,'egyik key ami kell'|'másik key ami kell'>
```

Readonly: Egy objektumtípus összes tulajdonságát csak olvashatóvá teszi.
https://www.typescriptlang.org/docs/handbook/utility-types.html#readonlytype

Record: Egy típust hoz létre, ahol egy adott kulcstípushoz egy adott értéktípus van hozzárendelve.
https://www.typescriptlang.org/docs/handbook/utility-types.html#recordkeys-type
```typescript
const data = [{name:"Joe",bornInYear:1985},{name:"Joe",bornInYear:1985}];
// form this array to an object using reduce:
const result = data.reduce((accu : Record<number,{name:string,bornInYear:number}>,curr,index)=>{
  accu[index] = {...curr};
  return accu;
},{})
// result típusa az accu típusa lesz, tehát egy szám kulcsú, {name:string,bornInYear:number} értékű objektum
```

Template Literal Types: Lehetővé teszi, hogy string típusokat építsünk sablonok segítségével, hasonlóan a JavaScript sablon stringjeihez, de típusokhoz használva.
https://www.typescriptlang.org/docs/handbook/2/template-literal-types.html
```typescript
  type ABC = "A"|"B"|"C";
  type OneTwoTree = 1|2|3;
  type ABC_123_Permutations = `${ABC}-${OneTwoTree}`;
  // type ABC_123_Permutations = "A-2" | "A-1" | "A-3" | "B-2" | "B-1" | "B-3" | "C-2" | "C-1" | "C-3"
```

ThisType: Egy marker interfész, amely lehetővé teszi a this pontosabb típusozását objektum literálokban vagy osztálymetódusokban.
https://www.typescriptlang.org/docs/handbook/utility-types.html#thistypetype

Parameters: Egy függvény paramétereinek típusait vonja ki.
https://www.typescriptlang.org/docs/handbook/utility-types.html#parameterstype
```typescript
function parameteresFunkcio(arg1:string,arg2:string){
  return {arg1,arg2};
}
//így egy tömböt ad vissza:
type CreateUserInputArr = Parameters<typeof parameteresFunkcio> // [arg1:string,arg2:string]
// Így csak az elsőt 
type CreateUserInput = Parameters<typeof parameteresFunkcio>['0'] // arg1:string
```

ReturnType: Egy függvény visszatérési típusát vonja ki.
https://www.typescriptlang.org/docs/handbook/utility-types.html#returntypetype
```typescript
function f1(): { a: number; b: string }{/*logic here*/};
type T4 = ReturnType<typeof f1>; // { a: number; b: string }

type T2 = ReturnType<<T>() => T>; // itt: unknown
type T6 = ReturnType<never>; // itt: never, mert a never megadható funkcióként is
// de sok mindent adhat vissza, void-ot, ha nincs visszatérési érték, vagy egyebeket,
// linken meg kell nézni
```

Required: Adott típuson belül minden opcionális értéket kötelezővé változtat:
https://www.typescriptlang.org/docs/handbook/utility-types.html#requiredtype
```typescript
type KotelezoMidenMezo = Required<VannakOpcionalisMezok>;
```