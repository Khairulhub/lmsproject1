Multiple user 🧮 
  AuthenticatedSessionController {
    <!-- changer this code first code is that you need to change it  -->
    public function store(LoginRequest $request): RedirectResponse
    {
        $request->authenticate();

        $request->session()->regenerate();

        return redirect()->intended(RouteServiceProvider::HOME);
    }



    <!-- changed code is here  -->


     $request->authenticate();

        $request->session()->regenerate();
        
        $url = '';
        if($request->user()->role === 'admin'){
            $url = 'admin/dashboard';  
        }
        elseif($request->user()->role === 'instructor'){ // Corrected 'instractor' to 'instructor'
            $url = 'instructor/dashboard'; // Corrected 'instractor' to 'instructor'
        }
        elseif($request->user()->role === 'user'){ // Corrected 'user' to 'user
            $url = '/dashboard';
        }
    
        return redirect()->intended($url);
  }