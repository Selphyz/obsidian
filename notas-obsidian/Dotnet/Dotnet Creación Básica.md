```
dotnet new sln --name Restaurants
```

# Crear API con Swashbuckle

```
dotnet new webapi --name Restaurants.API --output Restaurants.API
```
# Crear el resto de los proyectos de biblioteca de clases

```
dotnet new classlib --name Restaurants.Application --output Restaurants.Application

dotnet new classlib --name Restaurants.Domain --output Restaurants.Domain

dotnet new classlib --name Restaurants.Infrastructure --output Restaurants.Infrastructure
```

# Añadir proyectos a la solución

```
dotnet sln add **/*.csproj
```


# Añadir referencias entre proyectos

```
dotnet add Restaurants.API/Restaurants.API.csproj reference Restaurants.Application/Restaurants.Application.csproj

dotnet add Restaurants.API/Restaurants.API.csproj reference Restaurants.Infrastructure/Restaurants.Infrastructure.csproj

dotnet add Restaurants.Application/Restaurants.Application.csproj reference Restaurants.Domain/Restaurants.Domain.csproj

dotnet add Restaurants.Infrastructure/Restaurants.Infrastructure.csproj reference Restaurants.Application/Restaurants.Application.csproj
```