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




  <!-- protect route ar jonno code  -->
  // frontend Admin part 

//admin middleware protected role 
Route::middleware(['auth','roles:admin'])->group(function(){
    Route::get('/admin/dashboard', [AdminController::class, 'index'])->name('admin.dashboard');
});


//create a middleware Role and make some changes 
public function handle(Request $request, Closure $next, $role): Response
    {
        if($request->user()->role !== $role){
            return redirect('dashboard');
        }
        return $next($request);
    }


// then add the middleware to the kernel because it need to call any time so it need to update it 
 protected $middlewareAliases = [
        'auth' => \App\Http\Middleware\Authenticate::class,
        'roles' => \App\Http\Middleware\Role::class,
        'auth.basic' => \Illuminate\Auth\Middleware\AuthenticateWithBasicAuth::class,
        'auth.session' => \Illuminate\Session\Middleware\AuthenticateSession::class,
        'cache.headers' => \Illuminate\Http\Middleware\SetCacheHeaders::class,
        'can' => \Illuminate\Auth\Middleware\Authorize::class,
        'guest' => \App\Http\Middleware\RedirectIfAuthenticated::class,
        'password.confirm' => \Illuminate\Auth\Middleware\RequirePassword::class,
        'precognitive' => \Illuminate\Foundation\Http\Middleware\HandlePrecognitiveRequests::class,
        'signed' => \App\Http\Middleware\ValidateSignature::class,
        'throttle' => \Illuminate\Routing\Middleware\ThrottleRequests::class,
        'verified' => \Illuminate\Auth\Middleware\EnsureEmailIsVerified::class,
    ];


    #by using this user can not inter the instractor and admin dashboard also instracoor can not inter the admin dashboard.

    