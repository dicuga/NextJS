# Configuración básica NextJS + MUI

## Instalaciones
```
yarn create next-app --typescript

yarn add @mui/material @emotion/react @emotion/styled
yarn add @mui/icons-material

yarn add axios
```

## Borrar:
```
Fichero:
  styles/home.module.css
```

```
Borrar contenido completo de:
  styles/globals.css
```

## pages/index.tsx:
```
import { Layout } from "@/components/layouts/layout";

export default function Home() {
  return (
    <Layout>
      <h1>Hola mundo</h1>
    </Layout>
  )
}
```

## pages/_documents.tsx:
```
import { Html, Head, Main, NextScript } from 'next/document'

export default function Document() {
  return (
    <Html lang="en">
      <Head>
        <link
          rel="stylesheet"
          href="https://fonts.googleapis.com/css?family=Roboto:300,400,500,700&display=swap"
        />
      </Head>
      <body>
        <Main />
        <NextScript />
      </body>
    </Html>
  )
}
```

## Crear carpeta themes/basic-theme.ts
```
import { createTheme } from '@mui/material';

export const basicTheme = createTheme({
  palette: {
    mode: 'light'
  }
});
```

## pages/_app.tsx debe quedar así:
```
import '@/styles/globals.css'
import type { AppProps } from 'next/app'
import { CssBaseline, ThemeProvider } from '@mui/material'
import { basicTheme } from '@/themes/basic-theme'

export default function App({ Component, pageProps }: AppProps) {
  return (
    <ThemeProvider theme={basicTheme}>
      <CssBaseline />
      <Component {...pageProps} />
    </ThemeProvider>
  )
}
```

## Creamos las siguientes carpetas
```
components
	layouts
	ui
config
context
```

## config/clienteAxios.ts
```
import axios from 'axios';
    
const clienteAxios = axios.create({
    baseURL: '/api'
});

export default clienteAxios;
```

## components/layouts/Layout.tsx
```
import { FC } from 'react'
import Head from 'next/head'
import { Box } from '@mui/material'
import { Navbar } from '../ui';

interface Props {
  children: React.ReactNode;
  title?: string;
}

export const Layout: FC<Props> = ({title = 'Titulo app.....', children}) => {
  return (
    <Box sx={{ flexFlow: 1}}>
      <Head>
        <title>{ title }</title>
      </Head>
      
      <Navbar />
      <Box sx={{ padding: '10px 20px'}}>
        { children }
      </Box>
      
    </Box>
  )
}
```

## components/ui/NavBar.tsx
```
import NextLink from 'next/link';
import { AppBar, IconButton, Toolbar, Typography, Link } from '@mui/material';
import { MenuOutlined } from '@mui/icons-material';

export const Navbar = () => {
  return (
    <AppBar position='sticky' elevation={0}>
      <Toolbar>
        <IconButton
          size='large'
          edge='start'
        >
          <MenuOutlined />
        </IconButton>
        <NextLink href="/" passHref>
          <Link underline='none' color="white">
            <Typography variant='h6'>MENU</Typography>
          </Link>
        </NextLink>
      </Toolbar>
    </AppBar>
  )
}
```

