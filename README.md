# CURSO: APRENDE BLAZOR

# LECCIÓN 33: Componente NavigationManager (Parte 4)

1. Abrir la aplicación con Visual Studio 2022 o VSCode

2. El evento **NavigationManager.LocationChanged** te permite gestionar el evento que se genera al cambiar una ruta, es decir, su URL. Por ejemplo, mediante los botones de navegación del buscador de internet, mediante código o mediante la introducción de una nueva URL en la barra de búsqueda del navegador de Internet.

5. Este es un ejemplo para ilustrar el eento **NavigationManager.LocationChanged**

```razor
@page "/"

<PageTitle>Home</PageTitle>

@implements IDisposable

@code {
    [Inject] private NavigationManager? NavigationManager { get; set; }
    private string? currentUri;
    private DateTime navigationTime;

    protected override void OnInitialized()
    {
        // Get the current URI
        currentUri = NavigationManager.Uri;

        // Subscribe to the LocationChanged event
        NavigationManager.LocationChanged += OnLocationChanged;
    }

    private void OnLocationChanged(object sender, LocationChangedEventArgs e)
    {
        // Update the current URI and navigation time
        currentUri = e.Location;
        navigationTime = DateTime.Now;

        // Notify the UI to refresh
        InvokeAsync(StateHasChanged);
    }

    public void Dispose()
    {
        // Unsubscribe from the event when the component is disposed
        NavigationManager.LocationChanged -= OnLocationChanged;
    }
}
```
