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

Két fajtája van:

- SVG alapú ikonok (Material Icon)
- Szöveg-karakter alapú ikonok (Icon)

#### Material Icon

Ezt külön kell telepíteni

```
  npm install @mui/icons-material
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
* color="primary"\
A szokásos színsémák
* fontSize="small"\
Érdekes módon hiába SVG, mégis font-size-nak hívják.
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
