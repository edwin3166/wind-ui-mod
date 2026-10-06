# WindUI Hybrid

Versión alternativa no oficial de [WindUI](https://github.com/Footagesus/WindUI) 1.6.66 que activa por defecto el estilo nuevo de los elementos (toggles, sliders y botones).

## Qué hace

- Carga WindUI 1.6.66 y, si falla, la rama `main`.
- Activa `NewElements` por defecto. Si quieres el estilo clásico, pon `NewElements = false` en `CreateWindow`.
- Reintenta si falla la red y tiene un tiempo límite por descarga.
- Guarda una copia local para usarla cuando GitHub no responda.
- Acepta `Desc` como `Content` en `Notify`.

No modifica el código de la librería original.

## Archivos

| Archivo | Para qué sirve |
| --- | --- |
| `WindUI-Hybrid.lua` | Loader pequeño. Es lo que cargas en tus scripts. |
| `main.lua` | Copia propia de WindUI 1.6.66 con `NewElements` activado por defecto (opcional). |

## Uso

```lua
local WindUI = loadstring(game:HttpGet("https://raw.githubusercontent.com/TU_USUARIO/TU_REPO/main/WindUI-Hybrid.lua"))()

local Window = WindUI:CreateWindow({
    Title = "Mi Hub",
    Folder = "MyHub",
    Theme = "Dark",
})

local Tab = Window:Tab({ Title = "Main", Icon = "house" })

Tab:Toggle({
    Title = "Toggle",
    Type = "Toggle", -- o "Checkbox"
    Value = false,
    Callback = function(v) print(v) end,
})

Tab:Slider({
    Title = "Slider",
    IsTooltip = true,
    IsTextbox = true,
    Step = 1,
    Value = { Min = 0, Max = 200, Default = 100 },
    Callback = function(v) print(v) end,
})

Tab:Button({
    Title = "Botón azul",
    Color = Color3.fromHex("#305dff"),
    Icon = "mouse",
    Callback = function() print("click") end,
})
```

## Configuración opcional

Escríbela antes de cargar el loader:

```lua
getgenv().WindUIHybrid = {
    Source = "https://raw.githubusercontent.com/TU_USUARIO/TU_REPO/main/main.lua", -- tu copia, se prueba primero
    NewElements = true,  -- false = estilo clásico por defecto
    Cache = true,        -- false = no guardar copia local
    PreferCache = false, -- true = arranque rápido con la copia local
    Retries = 2,         -- intentos por fuente
    Timeout = 15,        -- segundos máximos por descarga
    Debug = false,       -- true = muestra los pasos en la consola
}
```

Después de cargar, `WindUI.HybridInfo` indica de dónde salió la librería:

```lua
print(WindUI.HybridInfo.Source, WindUI.HybridInfo.FromCache, WindUI.HybridInfo.Version)
```

## Aviso

`loadstring` ejecuta el código que haya en ese enlace en el momento de cargar. Si quieres que el código no cambie nunca, usa tu propia copia (`main.lua`) en `Source`.

## Créditos y licencia

WindUI es obra de [Footagesus](https://github.com/Footagesus/WindUI) y se distribuye bajo licencia MIT. Este proyecto no está afiliado al autor original. Toda la librería pertenece a su autor; aquí solo se cambia el valor por defecto de `NewElements`.
