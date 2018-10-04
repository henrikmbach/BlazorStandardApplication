Jeg har brugt https://www.codemag.com/Article/1809061/Re-Assembling-the-Web-with-Web-Assembly-and-Blazor
(Rick Strahls artikel i Visual Studio Magazine) til at komme igang med Blazor.
Jeg har ogs� kigget p� https://blogs.msdn.microsoft.com/webdev/2018/03/22/get-started-building-net-web-apps-in-the-browser-with-blazor/
(msdn-blog, en komme-i-gang med Blazor artikel)

__Her er hvad jeg lavede fredag 7/9-2018:__

Man skal installere nogle prerequisites for at det virker:
  - Visual Studio 2017 update 7 eller senere (jeg har pt. 2017 Community update 8, 3. udgave (fuld version 15.8.3))
	- .Net Core Blazor Language Extension (tror jeg nok) - en extension til Visual Studio, der er i "Tools", "Extension and Updates" menuen

S� har jeg i Visual Studio lavet et nyt projekt "Asp.Net Core Web ..." og s� skal man i wizard'en markere "Blazor"

S� stod der i msdn-blog artiklen at F5 for at debugge ikke virker i Visual Studio, men at Ctrl-F5 (uden debugning)
fungerer. Jeg fik en "HTTP Error 502.5 - Process Failure" fejl i Edge browseren n�r jeg pr�vede med Ctrl-F5.
Jeg pr�vede i Visual Studio at �ndre standard browser til Chrome:
![](V�lgStandardBrowserIVisualStudio.PNG)
Jeg fik samme fejl.
S� pr�vede jeg at klikke p� det shortcut, der var i fejl-beskeden i browseren 
(https://docs.microsoft.com/en-us/aspnet/core/host-and-deploy/iis/troubleshoot?view=aspnetcore-2.1)
Der var ikke rigtig noget der fangede. Der var et punkt i shortcuttet "Application Event Log" og med
det fandt jeg en fejl "IIS Express AspNetCore Module" fejl med en errorcode 0x80004005.
Og med et s�gte jeg p� Google efter "blazor error code 0x80004005" og det f�rste hit (https://github.com/aspnet/Blazor/issues/1342) 
sagde at man enten skulle slette global.json eller �ndre den til at indeholde ens nuv�rende version af .Net Core.
I en Visual Studio Command Prompt kan man udf�re "dotnet --info" og med den fik min seneste version til 2.1.401,
s� jeg �ndrede global.json fra "sdk": { "version": "2.1.300" ...
                           til "sdk": { "version": "2.1.401"
Og s� virkede det "HURRA!".

Og F5 virker ogs�, s� Ctrl-F5 er �benbart ikke n�dvendigt.

__Her er hvad jeg lavede l�rdag 8/9-2018:__

Jeg pr�vede at lave en Markdown fil (.md). Jeg s�gte efter en Markdown add-in til
Visual Studio og Mads Kristensen har lavet en - og den fungerer fint - den viser
hvordan markdown filen ser ud ved siden af. Det fungerer fint.
Et par markdown ting jeg har l�rt: 
* \!\[](url) for at vise et billede, url kan bare v�re en lokal sti til filen.
* \__ (dobbelt understregning) for at lave en understregning af en tekst

__Her er hvad jeg lavede s�ndag 9/9-2018:__

__Tilf�jede projektet til mit github:__ Jeg ved sgu ikke helt hvad proceduren var
for det. Men det var noget med i Team Explorer at connecte til noget Github 
(man kunne kun logge ind i Github Enterprse, hvad jeg ikke har). M�ske skal man
h�jreklikke p� projektet i Solution Explorer og der v�lge "Add to source control"
og s� bliver man bedt om at v�lge mellem VSTS og Github. Ved at v�lge Github
sker der s� forskellige ting - check p� github.com viser at det lykkedes.

__Starte Visual Studio as Administrator:__ Det er �benbart n�dvendigt at starte
Visual Studio med Administrator rettigheder for at f.eks. kompilering virker. hmmm!
Hvis ikke man starter med Adminstrator rettigheder, s� virker det s�dant set. Man
skal bare trykke f.eks. Ctrl-F5 2 gange - f�rste gange staller den og der sker ingenting. 
Hvis man s� afbryder kompileringen f.eks. og trykker Ctrl-F5 igen, s� k�rer det fint.
Hvis man starter med Adminstrator rettigheder virker Ctrl-F5 f�rste gang!

Jeg har ogs� l�st til og med "Build your first app" i https://blazor.net/docs/tutorials/build-your-first-blazor-app.html. Forts�t med det.

__19/8-2018__
Jeg har pr�vet at finde lidt ud af hvad det her Bootstrap, som �benbart er med
Blazor som standard, hvordan man bruger det.
Jeg har kigget p� https://www.c-sharpcorner.com/article/working-with-bootstrap-buttons-and-badges/
og arbejdet ganske lidt med knapper (og brugt btn-primary og btn-danger tagget p� button 
i Counter.cshtml f.eks.). 
Det er filme ikke nemt at finde noget forklaring p� Bootstrap og Blazor.

__4/10-2018__
Jeg har idag opdateret til Blazor 0.6.0 (fra 0.5.1). Det gik fint - der skulle
bare �ndres version nummer i csproj filen 3 steder.

TODO:
* forts�tte med artiklen
* I SurveyPrompt.cshtml er der "\<span class="oi oi-pencil mr-2" aria-hidden="true">\</span> der viser nogen med en pencil i output. Jeg har pr�vet at rette det til f.eks. Airplane ved at erstatte pencil med airplane, men det virker ikke. Find ud af hvorfor. Der st�r ogs� "mr-2" og det ved jeg ikke hvad er - noget bootstrap m�ske?
* ... 
