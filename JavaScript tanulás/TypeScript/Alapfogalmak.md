Ez a gyűjtemény segíthet a TypeScript alapjainak megértésében és a gyakran használt szakkifejezések értelmezésében.

1. **Type** (Típus):  
   A típusok határozzák meg a változók és kifejezések értékének típusát (pl. `number`, `string`, `boolean`), segítve a kód típusbiztonságát.

2. **Type Annotation** (Típus annotáció):  
   A TypeScript-ben használható típusmegjelölés, amellyel egy változó vagy függvény visszatérési értékének típusát adhatjuk meg. Pl.: `let age: number = 30;`.

3. **Interface** (Interfész):  
   Egy struktúrát határoz meg, amely leírja az objektumok formáját. Segít abban, hogy a különböző objektumok következetesen ugyanazt az alakot kövessék. Pl.: 
   ```typescript
   interface Person {
     name: string;
     age: number;
   }
   ```

4. **Type Inference** (Típus kitalálás):  
   A TypeScript automatikusan kitalálja a változók típusát, még ha nem is adunk meg típus annotációt. Pl.: 
   ```typescript
   let name = 'John'; // A TypeScript automatikusan 'string' típusúnak veszi.
   ```

5. **Union Types** (Unió típusok):  
   Olyan típusok, amelyek több típus egyesítésével jönnek létre, lehetővé téve, hogy egy változó többféle típust is felvegyen. Pl.: 
   ```typescript
   let id: number | string;
   id = 101; // vagy
   id = '101';
   ```

6. **Generics** (Általános típusok):  
   Lehetővé teszi, hogy egy függvény vagy osztály többféle típusra is működjön. A generikus típusok lehetővé teszik a típusbiztos újrahasznosítható kódot. Pl.: 
   ```typescript
   function identity<T>(arg: T): T {
     return arg;
   }
   ```

7. **Enum** (Felsorolás):  
   Az `enum` egy olyan speciális adatstruktúra, amely lehetővé teszi, hogy egy csoport konstans értéket hozzunk létre, amelyeket név szerint azonosíthatunk. Pl.: 
   ```typescript
   enum Color {
     Red,
     Green,
     Blue
   }
   ```

8. **Modules** (Modulok):  
   A modulok különálló egységekbe szervezik a kódot, amelyeket importálni és exportálni lehet, megkönnyítve a kód újrahasznosíthatóságát és karbantarthatóságát.

9. **Type Alias** (Típus alias):  
   Egy névhez rendelt típusdefiníció, amely lehetővé teszi a komplex típusok rövidítéseit. Pl.: 
   ```typescript
   type Point = { x: number; y: number; };
   ```

10. **Never** (Soha):  
    Olyan típus, amelyet soha nem lehet értékül adni. Olyan helyzetekben használják, amikor egy függvény soha nem ad vissza értéket (pl. hibát dob, vagy végtelen ciklusban fut).

11. **Any** (Bármilyen):  
    Egy univerzális típus, amely bármilyen értéket elfogad. Ez gyengíti a típusbiztonságot, ezért érdemes óvatosan használni.

12. **Void**:  
    Olyan típus, amely azt jelzi, hogy egy függvény nem ad vissza értéket. Leggyakrabban függvényeknél használják, amelyek valamilyen mellékhatás miatt futnak (pl. logolás). Pl.: 
    ```typescript
    function logMessage(message: string): void {
      console.log(message);
    }
    ```

13. **Tuple** (Tupel):  
    Egy fix hosszúságú tömb, amely különböző típusú elemeket tartalmazhat. Pl.: 
    ```typescript
    let tuple: [string, number];
    tuple = ['hello', 42];
    ```

14. **Readonly** (Csak olvasható):  
    Ez egy olyan típusmódosító, amely biztosítja, hogy egy változó vagy tulajdonság csak olvasható legyen, tehát nem lehet új értéket adni neki.

15. **Optional Properties** (Opcionális tulajdonságok):  
    Egy interfészen belül megadhatunk olyan tulajdonságokat, amelyek nem kötelezőek, azaz hiányozhatnak az objektumból. Az ilyen tulajdonságok után kérdőjel kerül. Pl.: 
    ```typescript
    interface Person {
      name: string;
      age?: number; // Opcionális tulajdonság
    }
    ```

16. **Type Assertion** (Típus állítás):
    A TypeScriptben arra szolgál, hogy a fejlesztő kifejezetten megmondja a fordítónak, hogy egy adott érték milyen típusú, akkor is, 
    ha a TypeScript ezt nem tudja automatikusan felismerni. Két féle módon lehet:
    
   ```typescript
   // 1. as szintaxis:
   let value: any = "hello";
   let strLength: number = (value as string).length;
   // 2. <> szintaxis:
   let strLength: number = (<string>value).length; 
   ```

17. **Literal Type** (Szószerinti érék): 
    Olyan típus, amely konkrét értékeket reprezentál. Ez lehet például egy adott sztring, szám vagy boolean érték. 
    Segítségével egy változónak csak meghatározott értékeket lehet adni.
    ```typescript
    let direction: "north" | "south" | "east" | "west";
    direction = "north";  // Ez érvényes
    direction = "up";     // Ez hibát ad, mert nem része a megadott értékeknek
    ```

18. **Type Guard** (Típus őr): 
    Egy olyan módszer, amellyel ellenőrizheted egy érték típusát futásidőben. Ez segít a fordítónak meghatározni, 
    hogy egy adott blokkban milyen típusú a változó, így a kód biztonságosabbá és típus-tudatossá válik.
    Típusai:
    1. typeof operátor
      Segítségével alapvető primitív típusokat tudunk ellenőrizni: string, number, boolean, symbol, undefined, bigint, és function.
      ```typescript
      function isString(value: any): value is string {
       return typeof value === "string";
      }
      ```
    2. instanceof operátor
      Akkor használható, ha egy objektumot egy adott osztály példányaként szeretnénk ellenőrizni.
      ```typescript
      if (pet instanceof Dog) {
       pet.bark();  // Itt biztosan egy Dog példány
      }
      ```
    3. in operátor
      Segítségével ellenőrizheted, hogy egy objektumban létezik-e egy adott property. 
      Ez hasznos, ha különböző interfészekkel rendelkező objektumok közül kell kiválasztanod egy típust.
      ```typescript
      interface Fish {
      swim: () => void;
      }
      
      interface Bird {
      fly: () => void;
      }

      function move(animal: Fish | Bird) {
         if ("swim" in animal) {
            animal.swim();  // Itt biztosan egy Fish
         } else {
            animal.fly();   // Itt biztosan egy Bird
         }
      }
      ```
    4. Diszkriminált uniók
      Ez a módszer akkor működik, ha az unió típusoknak van egy közös, azonos típusú (például string vagy number) propertyjük, amely alapján diszkriminálhatjuk őket.
      ```typescript
      interface Square {
      kind: "square";
      size: number;
      }

      interface Rectangle {
      kind: "rectangle";
      width: number;
      height: number;
      }

      type Shape = Square | Rectangle;

      function area(shape: Shape) {
      if (shape.kind === "square") {
         return shape.size * shape.size;  // Itt biztosan egy Square
      } else {
         return shape.width * shape.height;  // Itt biztosan egy Rectangle
      }
      }
      ```
    5. Mélyazonosság ellenőrzés
      Ha két külön változónak csak egy közös típusa van, akkor azok === -el való ellenőrzése szavatolja, hogy
      csak a közös típus lehet azon az ágon.
      ```typescript
      function example(x: string | number, y: string | boolean) {
      if (x === y) {
         // biztosan 'string' az 'x' és az 'y' is.
      } else { }
      ```