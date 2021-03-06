## Adicionando uma página XAML para o seu projeto {#adicionando-uma-p-gina-xaml-para-o-seu-projeto}

Agora que você já viu alguns trechos de XAML, vamos olhar para uma página XAML no contexto de um programa completo. Em primeiro lugar, crie um projeto **Xamarin.Forms** chamado **CodePlusXaml** usando **Portable Class Library** do template do projeto.

Agora adicione um XAML ContentPage para o PCL. Veja como:

No Visual Studio, clique com o botão direito no projeto **CodePlusXaml** em **Solucion Explorer**. Selecione **Add &gt; New Item**. Na caixa de diálogo **Add New Ítem**, selecione **Visual C#** na lista central. Nomeie **CodePlusXamlPage.cs.**

No Xamarin Studio, clique com o botão direito no projeto **CodePlusXaml** em **Solution Explorer**. Selecione **Add &gt; New Item**. Na caixa de diálogo **Add New Item**, selecione a opção **Forms** e **Forms Content Page Xaml** na lista central. Nomeie CodePlusXamlPage.cs.

Em ambos os casos, são criados dois arquivos:

*   CodePlusXamlPage.xaml, o arquivo XAML; e
*   CodePlusXamlPage.xaml.cs, um arquivo C # (apesar da extensão dupla no nome do arquivo)

Na lista de arquivos, o segundo arquivo é recuado abaixo do primeiro, indicando a sua relação estreita. O arquivo C # é muitas vezes referida como o _code-behind_ do arquivo XAML. Ele contém código que suporta a marcação.

Esses dois arquivos ambos contribuem para uma classe chamada CodePlusXamlPage que deriva de ContentPage.

Vamos examinar o código da classe. Excluindo-se os usings, veja:

namespace CodePlusXaml

{

public partial class CodePlusXamlPage : ContentPage

{

public CodePlusXamlPage()

{

InitializeComponent();

}

}

}

Como podemos ver, é uma classe chamada CodePlusXamlPage que deriva de ContentPage, tal como previsto.

No entanto, a definição da classe inclui uma palavra-chave partial, que geralmente indica que esta é apenas uma parte da definição de classe CodePlusXamlPage. Em outro lugar deve haver uma outra definição de classe parcial para CodePlusXamlPage. Então, se ela existe, onde está? É um mistério! (Por enquanto.)

Outro mistério é o método InitializeComponent que o construtor chama. A julgar unicamente da sintaxe, parece que este método deve ser definido ou herdado por ContentPage. No entanto, você não vai encontrar InitializeComponent na documentação da API.

Vamos deixar esses dois mistérios de lado temporariamente e olhar para o arquivo XAML. O Visual Studio e o Xamarin Studio geram dois arquivos XAML um pouco diferentes. Se você estiver usando Visual Studio, altere as marcações da Label e substitua por ContentPage.Content property element tags de modo que ele se parece com a versão em Xamarin Studio:

&lt;ContentPage xmlns=&quot;[http://xamarin.com/schemas/2014/forms](http://xamarin.com/schemas/2014/forms)&quot; xmlns:x=&quot;[http://schemas.microsoft.com/winfx/2009/xaml](http://schemas.microsoft.com/winfx/2009/xaml)&quot; x:Class=&quot;CodePlusXaml.CodePlusXamlPage&quot;&gt;

&lt;ContentPage.Content&gt;

&lt;/ContentPage.Content&gt;

&lt;/ContentPage&gt;

O elemento raiz é ContentPage, que é a classe que CodePlusXamlPage deriva. Essa tag começa com duas declarações de namespace XML, sendo que ambos são URIs. Mas não se incomode em verificar os endereços da web! Não há nada lá. Esses URIs simplesmente indicam que é dono do domínio e qual a função.

O namespace padrão pertence à Xamarin. Este é o namespace XML para elementos do arquivo com nenhum prefixo, como o tag ContentPage. A URL inclui o ano em que este domínio surgiu e a palavra forms como uma abreviação para Xamarin.Forms.

O segundo namespace está associado com um prefixo de x por convenção, e que pertence a Microsoft. Este namespace refere-se a elementos e atributos que são intrínsecos à XAML e são encontrados em todas as Implementação XAML. A palavra WinFX refere-se a um nome uma vez utilizado para o .NET Framework 3.0, que introduziu WPF e XAML. O ano de 2009 refere-se a uma especificação XAML particular, o que também implica uma coleção particular de elementos e atributos que constroem em cima da especificação XAML original, que é datada de 2006\. No entanto, Xamarin.Forms implementa apenas um subconjunto dos elementos e atributos na especificação de 2009\.

A próxima linha é um dos atributos que é intrínseco a XAML, chamados de Class. Porque o prefixo x é quase universalmente utilizado para este namespace, este atributo é comumente referido como x: Class e pronunciada &quot;X class.&quot;

O atributo x:class pode aparecer apenas no elemento raiz de um arquivo XAML. Ele especifica o .NET e suas classes derivadas. A classe base desta classe derivada é o elemento raiz. em Ou seja, a especificação deste x:Class indica que a classe no CodePlusXamlPage no CodePlusXaml deriva ContentPage. Essa é exatamente a mesma definição de classe CodePlusXamlPage no arquivo CodePlusXamlPage.xaml.cs.

Vamos adicionar algum conteúdo, o que significa a criação de algo para o Content property, que no Arquivo XAML significa colocar algo entre ContentPage.Content e no property-element tags. Inicie o conteúdo com um StackLayout, e em seguida, adicione um Label para o Children property:

&lt;ContentPage xmlns=&quot;[http://xamarin.com/schemas/2014/forms](http://xamarin.com/schemas/2014/forms)&quot; xmlns:x=&quot;[http://schemas.microsoft.com/winfx/2009/xaml](http://schemas.microsoft.com/winfx/2009/xaml)&quot; x:Class=&quot;CodePlusXaml.CodePlusXamlPage&quot;&gt;

&lt;ContentPage.Content&gt;

&lt;StackLayout&gt;

&lt;StackLayout.Children&gt;

&lt;Label Text=&quot;Hello from XAML!&quot; IsVisible=&quot;True&quot; Opacity=&quot;0.75&quot; XAlign=&quot;Center&quot;

VerticalOptions=&quot;CenterAndExpand&quot; TextColor=&quot;Blue&quot; BackgroundColor=&quot;#FF8080&quot; FontSize=&quot;Large&quot; FontAttributes=&quot;Bold,Italic&quot; /&gt;

&lt;/StackLayout.Children&gt;

&lt;/StackLayout&gt;

&lt;/ContentPage.Content&gt;

&lt;/ContentPage&gt;

Essa é a Label XAML que você viu no início deste capítulo

Agora você vai precisar alterar a classe App para instanciar esta página assim como você faz com um code-only derivado de ContentPage:

namespace CodePlusXaml

{

public class App : Application

{

public App()

{

MainPage = new CodePlusXamlPage();

}

…

}

}

Agora você pode fazer build e deploy este programa. Depois de fazer isso, é possível esclarecer um par de mistérios:

Em Visual Studio, no **Solution Explorer**, selecione o projeto **CodePlusXaml**, e clique no ícone na parte superior com o tooltip Show All Files.

Em Xamarin Studio, na lista de arquivos **Solution**,acessar o menu drop-down para toda a solução, e selecione **Display Options &gt; Show All Files**.

No projeto **CodePlusXaml** Portable Class Library, localize a pasta **obj** e dentro dela, a pasta **Debug**. Você verá um arquivo chamado CodePlusXamlPage.xaml.g.cs. Observe o g no nome do arquivo. Isso significa gerado. Aqui está ele, completo com o comentário que diz que este arquivo é gerado por uma ferramenta:

//------------------------------------------------------------------------------

// &lt;auto-generated&gt;

// This code was generated by a tool.

// Runtime Version:4.0.30319.35317

//

// Changes to this file may cause incorrect behavior and will be lost if

// the code is regenerated.

// &lt;/auto-generated&gt;

//------------------------------------------------------------------------------

namespace CodePlusXaml

{

using System;

using Xamarin.Forms;

using Xamarin.Forms.Xaml;

public partial class CodePlusXamlPage : ContentPage

{

private void InitializeComponent()

{

this.LoadFromXaml(typeof(CodePlusXamlPage));

}

}

}

Durante o processo de compilação, o arquivo XAML é analisado, e este arquivo de código é gerado. Observe que é uma definição de classe parcial de CodePlusXamlPage, que deriva de ContentPage, e a classe contém um método chamado InitializeComponent.

Em outras palavras, é um ajuste perfeito para o arquivo de code-behind CodePlusXamlPage.xaml.cs. após o arquivo CodePlusXamlPage.xaml.g.cs ser gerado, os dois arquivos podem ser compilados em conjunto como se fossem apenas C # normal. O arquivo XAML não tem outro papel no processo de construção, mas o todo o arquivo XAML está vinculado para o executável como um recurso incorporado (assim como o Edgar Allan Poe exemplificou no programa **BlackCat** no Capítulo 4).

Em tempo de execução, a classe App instancia a classe CodePlusXamlPage. O construtor CodePlusXamlPage (Definido no arquivo code-behind) chama InitializeComponent (definido no arquivo gerado), e InitializeComponent chama LoadFromXaml. Este é um método de extensão View definido nas extensões de classe do Xamarin.Forms.Xaml. LoadFromXaml carrega o arquivo XAML (que você vai se lembrar é vinculado para o executável como um recurso incorporado) e analisa-lo pela segunda vez. Porque esta análise ocorre em tempo de execução, LoadFromXaml pode instanciar e inicializar todos os elementos do arquivo XAML, exceto para o elemento de raiz, o que já existe. Quando o InitializeComponent método retorna, toda a página estará no lugar, como se tudo tivesse sido instanciado e inicializado em código no construtor CodePlusXamlPage.

É possível continuar a adicionar conteúdo à página após o retorno do InitializeComponent no construtor do arquivo code-behind. Vamos usar esta oportunidade para criar outra label usando algum código anterior neste capítulo:

namespace CodePlusXaml

{

public partial class CodePlusXamlPage : ContentPage

{

public CodePlusXamlPage()

{

InitializeComponent();

Label label = new Label

{

Text = &quot;Hello from Code!&quot;, IsVisible = true,

Opacity = 0.75,

XAlign = TextAlignment.Center,

VerticalOptions = LayoutOptions.CenterAndExpand, TextColor = Color.Blue,

BackgroundColor = Color.FromRgb(255, 128, 128),

FontSize = Device.GetNamedSize(NamedSize.Large, typeof(Label)), FontAttributes = FontAttributes.Bold | FontAttributes.Italic

};

(Content as StackLayout).Children.Insert(0, label);

}

}

}

O construtor conclui acessando o StackLayout que sabemos que está definido para o Content property da página e inserindo a label na parte superior. (No próximo capítulo, você verá melhores maneiras de fazer referência a objetos no arquivo XAML usando o atributo x:Name) Você pode criar a label antes da chamada InitializeComponent, mas você não pode adicioná-lo à StackLayout porque InitializeComponent é o que faz com que o Stacklayout (e todos os outros elementos XAML) seja instanciado. Aqui está o resultado:

![Three side-by-side screenshots showing the XAML Hello program on iPhone, Android, and Windows Phone.](../assets/three_side-by-side_screenshots_show.jpeg)

Além do texto, os dois botões são idênticos.

Você não tem que gastar muito tempo examinando o arquivo de código gerado que o analisador XAML cria, mas é útil entender como o arquivo XAML desempenha um papel tanto no processo de construção e durante tempo de execução. No entanto, às vezes um erro na chamada do arquivo XAML gera uma exceção de tempo de execução no LoadFromXaml, então você provavelmente vai ver o arquivo de código gerado aparecer com freqüência, e você deve saber o que é.