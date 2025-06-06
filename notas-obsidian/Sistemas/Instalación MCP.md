
Instalacion del MCP de Superset a través del instalador de MPCs Smithery
```
npx -y @smithery/cli install @aptro/superset-mcp --client claude
```
Una vez Claude Desktop detecte las herramientas. Claude necesita primero authenticarte con Superset. Deberias de configurar las variables de entorno siguientes compatibles con la instancia de Superset en cuestión.

```bash
export SUPERSET_USERNAME="tu_usuario" 
export SUPERSET_PASSWORD="tu_contraseña" 
export SUPERSET_BASE_URL="http://localhost:8088"
```

```powershell
$env:SUPERSET_USERNAME="tu_usuario" 
$env:SUPERSET_PASSWORD="tu_contraseña" $env:SUPERSET_BASE_URL="http://localhost:8088"
```
Archivo .env en tu directorio de trabajo o perfil de usuario. O también variables de sistema a la antigua desde "Propiedades del sistema" en Windows
```
SUPERSET_USERNAME=tu_usuario 
SUPERSET_PASSWORD=tu_contraseña 
SUPERSET_BASE_URL=http://localhost:8088
```
