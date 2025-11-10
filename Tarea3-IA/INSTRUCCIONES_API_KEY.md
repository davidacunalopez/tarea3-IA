# Instrucciones para Configurar la API Key de OpenAI

## 📍 Dónde agregar la API Key de OpenAI

La API Key de OpenAI debe configurarse en **dos lugares principales**:

### 1. **En Google Colab Secrets (Recomendado)**

**Ubicación en el notebook:** Celda 24 (Paso 2: Configuración del modelo OpenAI)

**Pasos:**
1. En Google Colab, haz clic en el icono de **🔒 (candado)** en la barra lateral izquierda
2. Haz clic en **"Add new secret"**
3. Nombre del secreto: `OPENAI_API_KEY`
4. Valor: Pega tu API key de OpenAI (formato: `sk-...`)
5. Guarda el secreto

El código en la celda 24 automáticamente leerá la key desde Colab Secrets:
```python
from google.colab import userdata
OPENAI_API_KEY = userdata.get('OPENAI_API_KEY')
```

### 2. **Como Variable de Entorno (Alternativa)**

Si prefieres no usar Colab Secrets, puedes configurarla directamente en el código:

**Ubicación:** Celda 24, después de la línea `OPENAI_API_KEY = userdata.get('OPENAI_API_KEY')`

Agrega esta línea:
```python
# Si no está en Secrets, configúrala aquí:
if not OPENAI_API_KEY:
    os.environ['OPENAI_API_KEY'] = 'sk-tu-api-key-aqui'
    OPENAI_API_KEY = os.environ['OPENAI_API_KEY']
```

### 3. **En la Interfaz Streamlit (Para la aplicación web)**

**Ubicación:** Celda 31 (Interfaz Streamlit)

La aplicación Streamlit tiene un campo en el sidebar donde puedes ingresar la API key directamente:
- Abre la aplicación Streamlit
- En el sidebar, busca el campo **"OpenAI API Key"**
- Ingresa tu API key allí

## ✅ Verificación

Después de configurar la API key, ejecuta la celda 24. Deberías ver:
```
✅ OpenAI API Key configurada
```

Si ves un mensaje de advertencia, revisa que:
- El nombre del secreto sea exactamente `OPENAI_API_KEY` (sin espacios, mayúsculas correctas)
- La API key sea válida y tenga el formato correcto (`sk-...`)

## 🔑 Obtener tu API Key de OpenAI

1. Ve a https://platform.openai.com/api-keys
2. Inicia sesión en tu cuenta de OpenAI
3. Haz clic en **"Create new secret key"**
4. Copia la key (solo se muestra una vez)
5. Pégala en Colab Secrets o en el código según tu preferencia

## ⚠️ Importante

- **NUNCA** compartas tu API key públicamente
- **NUNCA** la subas a repositorios públicos de GitHub
- La API key tiene límites de uso según tu plan de OpenAI
- Si excedes los límites, verás errores 429 (Rate Limit Exceeded)

