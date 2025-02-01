
Az Enumok olyan ritka kivételek a typescriptben, amik nem csak a típusokat határozzák meg, hanem értékeik is vannak. Az értékek konstansok, amelyeknek neveik vannak (objektumokhoz hasonlóan).

_________________________________
NUMERIC ENUMS - Számozott enum-ok

Itt az enum nevekhez konstans számok tartoznak.
Ha nem adunk meg külön értéket, akkor 0-tól kezdve 1-el növelve kapják a felsorolt változónevek a számértékeket:

```typescript
enum Direction {
  Up, //0
  Down, //1
  Left, //2
  Right, //3
}
```
De ha megadjuk az első értékét, akkor onnan indul a számolás:

```typescript
enum Direction {
  Up = 1, //1
  Down, //2
  Left, //3
  Right, //4
}
```

A TypeScript numeric enum (számozott felsorolás) típusát olyan helyzetekben használják, ahol egy adott értékkészletet szeretnénk reprezentálni számozott értékekkel. Gyakorlati példák:

 Jogosultsági szintek meghatározására:
```typescript
enum AccessLevel {
    Guest = 0,
    User = 1,
    Moderator = 2,
    Admin = 3
}

let userAccess: AccessLevel = AccessLevel.Moderator;
```
Hibakódok, státuszkódok vagy protokoll üzenetek:
Például HTTP státuszkódok használatára, ahol a kódok számokkal jelennek meg, de a programban olvasható formában tudjuk használni őket.

```typescript
enum HttpStatus {
    OK = 200,
    BadRequest = 400,
    Unauthorized = 401,
    NotFound = 404,
    InternalServerError = 500
}

let responseStatus: HttpStatus = HttpStatus.OK;

```
De használható számított értékekkel is, azonban ezek nem alkalmasak automatikus inkrementáció kezdőpontjának:

```typescript
enum E {
  A = getSomeValue(),
  B,
Error: Enum member must have initializer.
}
```
## STRING ENUMS - szöveg enumok
Ezek is konstansok, de mindegyiknek adni kell értéket (inicializálni kell). Hasznuk azonos a számozott verzióval, olvashatóbbá teszik a kódot.

```typescript
enum Direction {
  Up = "UP",
  Down = "DOWN",
  Left = "LEFT",
  Right = "RIGHT",
}
```