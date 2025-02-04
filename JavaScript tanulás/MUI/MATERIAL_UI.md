# Material UI komponensek

## Data display - adat megjelenítők:

### Typography

https://mui.com/material-ui/react-typography/
Szöveges tartalmak megjelenítésére. Mindet ezzel kell beállítani, de lehetnek variánsok a megjelenésben, és más-más komponst lehet lerenderelni velük.
Az alapbeállítás a component="p", azaz p-tag, és az annak megfelelő variant='body1'. Ha adtunk meg component-property-t, akkor pedig az annak megfelelő variáns.\
A variánsok lehetnek: h1-h6-ig, body1,body2,subtitle1,subtitle2,caption,button,overline, stb..

```typescript
   <Typography
       variant='h1' {/* Ez dönti el, hogy hogyan nézzen ki. Itt: H1 style-ja lesz */}
       component="h3" {/* Ilyen TAG-et generál a HTML kódba. */ }
       color="primary" {/*A színséma beállítás, nem egyenlő a CSS color szabállyal!*/}
     >
       Megjelenített szöveg
   </Typography>
```

Vannak általános, nem csak a Typography komponensben érvényes propertyk:

- color="primary"\
  Ennek értékei az előre megadott színsémák (theme color) nevei, mint primary, secondary, error, stb.
- align="center"\
  Értékei: right,left,center,justify
- noWrap\
  Ez azt jelenti, hogy nem tördeli a szöveget, egy sor marad, de overflow miatt ...-ra végződik.
- gutterBottom\
  Ekkor alul lesz margója csak.

### Ikonok

https://mui.com/material-ui/material-icons/?query=keyboardarr

Két fajtája van:

- SVG alapú ikonok (Material Icon)
- Szöveg-karakter alapú ikonok (Icon)

#### Material Icon

Ezt külön kell telepíteni, majd újra indítani a dev szervert, különben hibát jelez.

```
  npm install @mui/icons-material @mui/material @emotion/styled @emotion/react
```

5 különböző variánsa van, amiket mind külön kell importálgatni, mivel külön SVG-k. pl.:

```
import DeleteOutlinedIcon from '@mui/icons-material/DeleteOutlined';
import DeleteRoundedIcon from '@mui/icons-material/DeleteRounded';
import DeleteTwoToneIcon from '@mui/icons-material/DeleteTwoTone';
import DeleteSharpIcon from '@mui/icons-material/DeleteSharp';
import DeleteForeverIcon from '@mui/icons-material/DeleteForever';
```

Propertyk-:

- color="primary"\
  A szokásos színsémák
- fontSize="small"\
  Érdekes módon hiába SVG, mégis font-size-nak hívják.

##### Használatuk:

Lehet őket más komponensekben, pl. Button-okban használni ekkor lehet velük kezdeni, vagy a szöveg után tenni őket így:

```typescript
 <Button startIcon={<AcUnitIcon/>}>Szöveg előtti ikon</Button>
 <Button endIcon={<AcUnitIcon/>}>Szöveg utáni ikon</Button>
```

## Inputok

### Button

A szokásos HTML button, és az anchor 'a' tag MUI megfelelője.
3 fajta design-ja (variant-ja) van:

```typescript
  <>
  <Button href="#text-buttons">Link</Button> {/* Az <a> megfelelője */}
  <Button variant="contained">Contained </Button> {/* A kiemelt jelentőségű akciókhoz */}
  <Button variant="outlined">Outlined</Button>  {/* Másodlagos akciókhoz */}
```

Property-k:

- disabled\
  Ugyanaz, mint a HTML-ben.
- size="small"\
  A gomb mérete, 3 van: small,medium,large

#### Gomb, beágyazott ikonnal és címkével

Szöveg mellé lehet tenni ikonokat, amiknek a pozíciója lehet a szöveg kezdetére (startIcon), és végére (endIcon).

```typescript
<>
<Button variant="outlined" startIcon={<DeleteIcon />}>
Delete
</Button>
<Button variant="contained" endIcon={<SendIcon />}>
Send
</Button>
```

#### Ikongomb

Ezt az IconButton komponenssel kell használni, de amúgy azonos a többi.

```typescript
<IconButton aria-label="delete">
  <DeleteIcon />
</IconButton>
```

#### Button Group

Összetartozó gombok megfelelő elrendezésére való. A ButtonGroup-ban lehet egyszerre property-ket adni a gomboknak

```typescript
<ButtonGroup variant="contained" aria-label="Basic button group">
  <Button>One</Button>
  <Button>Two</Button>
  <Button>Three</Button>
</ButtonGroup>
// Itt minden gomb variant="contained"-ed lesz
```

## Layout elemek

### Container

Más elemeket tartalmazó komponens. Természetesen a child elemek a fontosak, de ad hozzá formázást.
Fajtái:

#### Fluid:

A maxWidth mindig 100%????

```typescript
<Container maxWidth="sm">
  <Box sx={{ bgcolor: "#cfe8fc", height: "100vh" }} />
</Container>
```

####Fixed container
Ez a min-width-hez alkalmazkodik, de ezt más szintaxissal kell megadni:

```typescript
  <Container fixed>
```

Property-k:

- component="main"\
  Itt lehet beállítani, hogy milyen html- Tag-be renderelje le a komonenst. Alapból div lesz.

# Stílusok

## makeStyles hook - nem támogatott már

Bárhová beimportálható kész stílusok készítésére való.
https://mui.com/system/styles/api/#makestyles-styles-options-hook

Elavult, helyette:
MUI System - Overview:\
https://mui.com/system/getting-started/

## Egyéni téma ~ Custom theme

https://mui.com/system/getting-started/the-sx-prop/

Egyéni témák létrehozására a createTheme funkció való.

### Színpaletták

A createTheme egy objektumot vár, amiben a palette címke alatt lehet a téma lehetséges palettáit meghatározni. (???Ha egy beépített stílust használunk, akkor csak felülírni???)
Így:

```typescript
import { Box, ThemeProvider, createTheme } from "@mui/system";

const theme = createTheme({
  palette: {
    // Ez a kötelező key a palettákhoz
    background: {
      // Ez egy custom paletta név
      paper: "#fff", // Ez a szín a palettában
    },
    text: {
      primary: "#173A5E",
      secondary: "#46505A",
    },
  },
});

export default function Example() {
  return (
    <ThemeProvider theme={theme}>
      {" "}
      {/* Használni a ThemeProvider-etl lehet */}
      <Box
        sx={{
          bgcolor: "background.paper", // itt fértünk hozzá a megadott színhez
          boxShadow: 1,
          borderRadius: 2,
          p: 2,
          minWidth: 300,
        }}
      ></Box>
    </ThemeProvider>
  );
}
```

Az adott komponensben úgy tehetjük elérhetővé a custom theme-et, hogy egy 'ThemeProvider'- Tag-be foglaljuk, amelynek megadjuk a téma nevét: 'theme={themeName}'

A legtöbb MUI komponens CSS-einek személyre szabásához használható az 'sx' property.

```typescript
<Box sx={{ color: "text.secondary" }}>Sessions</Box>
```

### Theme-aware properties

Olyan MUI specifikus property-k, amik a megjelenítéshez kapcsolódnak. Ezek nem egyenlőek a CSS értékekkel akkor se, ha azonos néven szerepelnek. Ezek közül a fontosabbak:

#### Borders

- border

```typescript
<Box sx={{ border: 1 }} />
// equivalent to border: '1px solid black'
```

- borderColor

```typescript
<Box sx={{ borderColor: "primary.main" }} />
// equivalent to borderColor: theme => theme.palette.primary.main
```

- borderRadius

```typescript
<Box sx={{ borderRadius: 2 }} />
// equivalent to borderRadius: theme => 2 * theme.shape.borderRadius
// default theme.shape.borderRadius is 4px
```

#### Grid

- gap, rowGap, columnGap

```typescript
<Box sx={{ gap: 2 }} />
// equivalent to gap: theme => theme.spacing(2) or theme.spacing * 2
// default valu of theme.spacing is 8px
```

#### Positions

- zIndex

```typescript
<Box sx={{ zIndex: "tooltip" }} />
// equivalent to zIndex: theme => theme.zIndex.tooltip
```

#### Shadows

- boxShadow\
  A box-shadow CSS-t módosítja 0-25-ig terjed a skála.

```typescript
<Box sx={{ boxShadow: 0 }}>…
<Box sx={{ boxShadow: 1 }}>…
<Box sx={{ boxShadow: 2 }}>…
<Box sx={{ boxShadow: 3 }}>…
```

#### Sizing

- width, height, minHeight, maxHeight, minWidth, maxWidth\
  Ha az ezekben megadott érték 0 és 1 közé esik, akkor %-nak értelmeződik, ha 1-nél nagyobb szám, akkor pixelnek.

```typescript
<Box sx={{ width: 1/2 }} /> // equivalent to width: '50%'
<Box sx={{ width: 20 }} /> // equivalent to width: '20px'
```

#### Spacing

theme.spacing értéket szorozzák meg a property-ben beadott értéket, (az apalértelmezett 8px)

- margin\
  A CSS azonosak rövidítve vannak a kezdő betűkre:

```
m  azaz	margin
mt azaz	margin-top
mr azaz	margin-right
mb azaz	margin-bottom
ml azaz	margin-left
```

És vannak összevont alakok az X és Y tengely mentén:

```
mx azaz	margin-left, margin-right
my azaz	margin-top, margin-bottom
```

- padding\
  A marginhoz hasoló rövidítések:

```
p	padding
pt	padding-top
pr	padding-right
pb	padding-bottom
pl	padding-left
px	padding-left, padding-right
py	padding-top, padding-bottom
```

#### Typography

Ide tartozik a fontFamily, fontSize, fontStyle, fontWeight propertyk. Ezeknek az értéke a theme.typography-ban tárolható.

```typescript
<Box sx={{ fontWeight: "fontWeightLight" }} />
// equivalent to fontWeight: theme.typography.fontWeightLight
```

#### Responsive values

Az sx property-ben megadhatók Responsive töréspontok is, azaz hogy mekkora méretek mellett milyen értéket vegyen fel az adott property.\
#### Töréspontok módosítása:
A töréspontok azok a pixelben vett szélességek, amitől kezdve érvényesek a mértere vonatkozó szabályok. Alapértelmezetten a következők: 
```typescript
const theme = createTheme({
  breakpoints: {
    values: {
      xs: 0,
      sm: 600,
      md: 900,
      lg: 1200,
      xl: 1536,
    },
  },
});
```
Ezek módosíthatók, ha custom theme-et csinálunk.\
Akár teljesen más nevekkel is létrehozhatjuk ezeket, azonban ekkor a typeScript kedvéért a következő módon ki is kell törölni a korábbiakat:
~~~typescript
declare module '@mui/material/styles' {
  interface BreakpointOverrides {
    xs: false; // amit false-ra állítok, az törlődik
    sm: false;
    md: false;
    lg: false;
    xl: false;
    mobile: true; // Amit újonnan hozzádok, az legyen true
    tablet: true;
    laptop: true;
    desktop: true;
  }
}
~~~
https://mui.com/material-ui/customization/breakpoints/#api
