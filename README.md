# Blazor AuthenticationExample

The purpose of this app is to give myself a quick reference for implementing authentication in Blazor applications. 

It includs: 
1. [x] Protecting content within a page (see Counter page) 
2. [ ] Protecting menu items in the NavMenu (See Weather page)
3. [ ] Protecting an entire page that you should be redirected to login if not authenticated (See Secure page)
4. [x] Displaying user information in the top-bar once you are logged in. (or not)
5. [x] Implementing logout functionality.

# For later if interested
1. [ ] Getting user from a database and validating them there.
2. [ ] Auto-update the login page. Subscribe to the authentication state changes method.
3. [ ] 

# What I Learned
* If you are subscribing to an authentication state change, then you need to be in an component with `@rendermode InteractiveServer`
* You can't put `@rendermode InteractiveServer` on the main page, or main layout page, so for these pages you need to add a component that has it.
* When you use `builder.Services.AddScoped<AuthenticationStateProvider, CustomAuthenticationStateProvider>();` you are replacing the default authentication 
state provider with your own implementation. Every time you use `@inject AuthenticationStateProvider AuthStateProvider` you are getting an instance of your custom provider.
* But if you want to use the extended methods of your custom provider, you need to use `(CustomAuthenticationStateProvider)AuthenticationStateProvider`. The
reason is that you need to use the `AuthenticationStateProvider` or else the dependency injection won't work.(It just creates a new instance of 
your custom provider instead of using the one in DI container).   
    ### See example from `NavHeader.razor`:

    ```
    private void Logout()
    {
        CustomAuthenticationStateProvider customAuthProvider = (CustomAuthenticationStateProvider)AuthenticationStateProvider;
        customAuthProvider.Logout();
    }
    ```
