## O Projeto IOS {#o-projeto-ios}

Um projeto iOS normalmente contém uma classe que deriva de **UIApplicationDelegate**. No entanto, a biblioteca Xamarin.Forms.Platform.iOS define uma classe base denominada **FormsApplicationDelegate**. No projeto Hello.iOS, você verá esse arquivo AppDelegate.cs, aqui usando diretivas e comentários:

```
using Foundation;
using UIKit;
namespace Hello.iOS
{
 [Register("AppDelegate")]
 public partial class AppDelegate :
 global::Xamarin.Forms.Platform.iOS.FormsApplicationDelegate
 {
 public override bool FinishedLaunching(UIApplication app, NSDictionary options)
 {
 global::Xamarin.Forms.Forms.Init();
 LoadApplication(new App());
 return base.FinishedLaunching(app, options);
 }
 }
}
```

A substituição **FinishedLaunching** começa chamando o método Forms.Init definido no assemble Xamarin.Forms.Platform.iOS. Em seguida, chama um método LoadApplication \(definido pelo FormsApplicationDelegate\), passando a ele uma nova instância da classe App definido no PCL compartilhada. O objeto da página definido para a propriedade MainPage deste objeto App pode ser usado para criar um objeto do tipo UIViewController, que é responsável por renderizar o conteúdo da página.

