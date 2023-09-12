# Aprèn Python

![Logo - AprendePython](_static/img/logo-solo-aprendepython-small.png)

Curs gratuït per aprendre el llenguatge de programació **Python** amb un enfocament **pràctic**, incloent **exercicis** i cobertura per a diferents **nivells de coneixement**.

## Desenvolupament

Assegura't que tens instal·lat _Docker_ y _docker-compose_.

Construir la imatge del projecte:

```console
$ docker-compose build
```

### Documentació en `html` pel desenvolupament

Renderitzar la documentació en `html` amb **live-reload**:

```console
$ docker-compose up
```

Un cop que apareguen per pantalla els següents missatges:

```console
Serving on http://0.0.0.0:8000
Start watching changes
Start detecting changes
```

, ja es podrè accedir a http://127.0.0.1:8000/ per veure la documentació.

### Documentació en `html` per producció

Renderitzar la documentació completa en `html`:

```console
$ docker-compose run aprendepython make dirhtml
```

A l'acabar l'execució, es podrà trobar la documentació del curs en: `_build/dirhtml/`.

### Documentació en `pdf`

Generar la documentació en `pdf` a través de _Latex_:

```console
$ docker-compose run aprendepython make latexpdf
```

> ℹ️️ &nbsp; Aquest procès triga el seu temps, ja que la documentació és extensa.

A l'acabar l'execució, es podrà trobar la documentació en: `_build/latex/aprendepython.pdf`
