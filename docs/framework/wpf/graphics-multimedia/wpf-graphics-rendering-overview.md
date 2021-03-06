---
title: Visão geral da renderização de gráficos
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- graphics [WPF], rendering
- rendering graphics [WPF]
ms.assetid: 6dec9657-4d8c-4e46-8c54-40fb80008265
ms.openlocfilehash: 9d58aa973f7de6c073611e13f2889913ff26dd55
ms.sourcegitcommit: 267d092663aba36b6b2ea853034470aea493bfae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/21/2020
ms.locfileid: "80111914"
---
# <a name="wpf-graphics-rendering-overview"></a>Visão geral de renderização de gráficos do WPF
Este tópico fornece uma visão geral da camada visual do [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]. Foca-se no papel <xref:System.Windows.Media.Visual> da classe para [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] dar suporte no modelo.  

<a name="role_of_visual_object"></a>
## <a name="role-of-the-visual-object"></a>Função do objeto visual  
 A <xref:System.Windows.Media.Visual> classe é a abstração <xref:System.Windows.FrameworkElement> básica da qual cada objeto deriva. Ela também serve como o ponto de entrada para escrever novos controles em [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] e, de muitas formas, pode ser pensada como o HWND (identificador de janela) no modelo de aplicativo Win32.  
  
 O <xref:System.Windows.Media.Visual> objeto é [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] um objeto central, cuja função principal é fornecer suporte de renderização. Controles de interface do <xref:System.Windows.Controls.Button> <xref:System.Windows.Controls.TextBox>usuário, como <xref:System.Windows.Media.Visual> e , derivam da classe, e usá-lo para persistir seus dados de renderização. O <xref:System.Windows.Media.Visual> objeto fornece suporte para:  
  
- Exibição de saída: renderização do conteúdo de desenho persistentes e serializado de um visual.  
  
- Transformações: Realizando transformações em um visual.  
  
- Recorte: dar suporte à área de recorte para um visual.  
  
- Teste de clique: determinar se uma coordenada ou geometria está contida dentro dos limites de um visual.  
  
- Cálculos de caixa delimitadora: determinar o retângulo delimitador de um visual.  
  
 No entanto, o <xref:System.Windows.Media.Visual> objeto não inclui suporte para recursos de não renderização, tais como:  
  
- Manipulação de eventos  
  
- Layout  
  
- Estilos  
  
- Associação de dados  
  
- Globalização  
  
 <xref:System.Windows.Media.Visual>é exposta como uma classe abstrata pública da qual as classes infantis devem ser derivadas. A ilustração a seguir mostra a hierarquia dos objetos visuais que são expostos no [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
 ![Diagrama de classes derivadas do objeto visual](./media/wpf-graphics-rendering-overview/classes-derived-visual-object.png)
  
### <a name="drawingvisual-class"></a>Classe DrawingVisual  
 A <xref:System.Windows.Media.DrawingVisual> é uma classe de desenho leve que é usada para renderizar formas, imagens ou texto. Essa classe é considerada leve porque não fornece layout ou manipulação de eventos, o que melhora o desempenho de runtime. Por esse motivo, desenhos são ideais para telas de fundo e clip-art. O <xref:System.Windows.Media.DrawingVisual> pode ser usado para criar um objeto visual personalizado. Para obter mais informações, consulte [Usando objetos DrawingVisual](using-drawingvisual-objects.md).  
  
### <a name="viewport3dvisual-class"></a>Classe Viewport3DVisual  
 O <xref:System.Windows.Media.Media3D.Viewport3DVisual> fornece uma ponte <xref:System.Windows.Media.Visual> <xref:System.Windows.Media.Media3D.Visual3D> entre 2D e objetos. A <xref:System.Windows.Media.Media3D.Visual3D> classe é a classe base para todos os elementos visuais 3D. As <xref:System.Windows.Media.Media3D.Viewport3DVisual> obrigações que <xref:System.Windows.Media.Media3D.Viewport3DVisual.Camera%2A> você <xref:System.Windows.Media.Media3D.Viewport3DVisual.Viewport%2A> define um valor e um valor. A câmera permite que você exiba a cena. O visor estabelece o local para o qual a projeção é mapeada na superfície 2D. Para obter mais informações [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]sobre o 3D in , consulte [Visão geral de gráficos 3D](3-d-graphics-overview.md).  
  
### <a name="containervisual-class"></a>Classe ContainerVisual  
 A <xref:System.Windows.Media.ContainerVisual> classe é usada como recipiente <xref:System.Windows.Media.Visual> para uma coleção de objetos. A <xref:System.Windows.Media.DrawingVisual> classe deriva <xref:System.Windows.Media.ContainerVisual> da classe, permitindo que contenha uma coleção de objetos visuais.  
  
### <a name="drawing-content-in-visual-objects"></a>Desenhar conteúdo em objetos visuais  
 Um <xref:System.Windows.Media.Visual> objeto armazena seus dados de renderização como uma **lista de instrução de gráficos vetoriais**. Cada item na lista de instruções representa um conjunto de baixo nível de dados gráficos e recursos associados em um formato serializado. Há quatro tipos diferentes de dados de renderização que podem conter conteúdo de desenho.  
  
|Tipo de conteúdo de desenho|Descrição|  
|--------------------------|-----------------|  
|Gráficos vetoriais|Representa dados gráficos vetoriais <xref:System.Windows.Media.Pen> e quaisquer informações associadas. <xref:System.Windows.Media.Brush>|  
|Imagem|Representa uma imagem dentro de <xref:System.Windows.Rect>uma região definida por um .|  
|Glifo|Representa um desenho que <xref:System.Windows.Media.GlyphRun>renderiza um , que é uma seqüência de glifos de um recurso de fonte especificado. Este é o modo pelo qual o texto é representado.|  
|Vídeo|Representa um desenho que renderiza vídeo.|  
  
 O <xref:System.Windows.Media.DrawingContext> permite que <xref:System.Windows.Media.Visual> você preencha um com conteúdo visual. Quando você <xref:System.Windows.Media.DrawingContext> usa os comandos de desenho de um objeto, você está realmente armazenando um conjunto de dados de renderização que mais tarde serão usados pelo sistema gráfico; você não está desenhando para a tela em tempo real.  
  
 Quando você [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] cria um controle, como a <xref:System.Windows.Controls.Button>, o controle gera implicitamente dados de renderização para desenhar-se. Por exemplo, <xref:System.Windows.Controls.ContentControl.Content%2A> definir a <xref:System.Windows.Controls.Button> propriedade das causas do controle para armazenar uma representação de renderização de um glifo.  
  
 A <xref:System.Windows.Media.Visual> descreve seu conteúdo como <xref:System.Windows.Media.Drawing> um ou <xref:System.Windows.Media.DrawingGroup>mais objetos contidos dentro de um . A <xref:System.Windows.Media.DrawingGroup> também descreve máscaras de opacidade, transformações, efeitos de bitmap e outras operações que são aplicadas ao seu conteúdo. <xref:System.Windows.Media.DrawingGroup>as operações são aplicadas na seguinte <xref:System.Windows.Media.DrawingGroup.OpacityMask%2A>ordem <xref:System.Windows.Media.DrawingGroup.Opacity%2A> <xref:System.Windows.Media.DrawingGroup.BitmapEffect%2A>quando <xref:System.Windows.Media.DrawingGroup.ClipGeometry%2A> <xref:System.Windows.Media.DrawingGroup.GuidelineSet%2A>o conteúdo <xref:System.Windows.Media.DrawingGroup.Transform%2A>é renderizado: , , , , e depois .  
  
 A ilustração a seguir <xref:System.Windows.Media.DrawingGroup> mostra a ordem em que as operações são aplicadas durante a seqüência de renderização.  
  
 ![Ordem das operações do DrawingGroup](./media/graphcismm-drawinggroup-order.png "graphcismm_drawinggroup_order")  
Ordem das operações do DrawingGroup  
  
 Para obter mais informações, consulte a [Visão geral de objetos de desenho](drawing-objects-overview.md).  
  
#### <a name="drawing-content-at-the-visual-layer"></a>Conteúdo de desenho na camada visual  
 Você nunca instancia diretamente um; <xref:System.Windows.Media.DrawingContext> você pode, no entanto, adquirir um contexto <xref:System.Windows.Media.DrawingGroup.Open%2A?displayProperty=nameWithType> <xref:System.Windows.Media.DrawingVisual.RenderOpen%2A?displayProperty=nameWithType>de desenho a partir de certos métodos, tais como e . O exemplo a <xref:System.Windows.Media.DrawingContext> seguir <xref:System.Windows.Media.DrawingVisual> recupera um de a e usa-o para desenhar um retângulo.  
  
 [!code-csharp[drawingvisualsample#101](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingVisualSample/CSharp/Window1.xaml.cs#101)]
 [!code-vb[drawingvisualsample#101](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DrawingVisualSample/visualbasic/window1.xaml.vb#101)]  
  
#### <a name="enumerating-drawing-content-at-the-visual-layer"></a>Enumerar conteúdo de desenho na camada visual  
 Além de seus outros <xref:System.Windows.Media.Drawing> usos, os objetos também fornecem <xref:System.Windows.Media.Visual>um modelo de objeto para enumerar o conteúdo de a .  
  
> [!NOTE]
> Quando você está enumerando o conteúdo do <xref:System.Windows.Media.Drawing> visual, você está recuperando objetos, e não a representação subjacente dos dados de renderização como uma lista de instrução de gráficos vetoriais.  
  
 O exemplo a <xref:System.Windows.Media.VisualTreeHelper.GetDrawing%2A> seguir usa <xref:System.Windows.Media.DrawingGroup> o <xref:System.Windows.Media.Visual> método para recuperar o valor de a eenumerar-lo.  
  
 [!code-csharp[DrawingMiscSnippets_snip#GraphicsMMRetrieveDrawings](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/EnumerateDrawingsExample.xaml.cs#graphicsmmretrievedrawings)]  
  
<a name="how_visual_objects_are_used_to_build_controls"></a>
## <a name="how-visual-objects-are-used-to-build-controls"></a>Como objetos visuais são usados para compilar controles  
 Muitos dos objetos no [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] são compostos de outros objetos visuais, o que significa que eles podem conter diversas hierarquias de objetos descendentes. Muitos dos elementos da interface do usuário no [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], tais como controles, são compostos de múltiplos objetos visuais que representam diferentes tipos de elementos de renderização. Por exemplo, <xref:System.Windows.Controls.Button> o controle pode conter uma <xref:Microsoft.Windows.Themes.ClassicBorderDecorator> <xref:System.Windows.Controls.ContentPresenter>série <xref:System.Windows.Controls.TextBlock>de outros objetos, incluindo , e .  
  
 O código a <xref:System.Windows.Controls.Button> seguir mostra um controle definido na marcação.  
  
 [!code-xaml[VisualsOverview#VisualsOverviewSnippet1](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualsOverview/CSharp/Window1.xaml#visualsoverviewsnippet1)]  
  
 Se você enumerar os objetos visuais <xref:System.Windows.Controls.Button> que compõem o controle padrão, você encontraria a hierarquia de objetos visuais ilustrada abaixo:  
  
 ![Diagrama de hierarquia de árvore visual](./media/wpf-graphics-rendering-overview/visual-object-diagram.gif)
  
 O <xref:System.Windows.Controls.Button> controle <xref:Microsoft.Windows.Themes.ClassicBorderDecorator> contém um elemento, que <xref:System.Windows.Controls.ContentPresenter> por sua vez, contém um elemento. O <xref:Microsoft.Windows.Themes.ClassicBorderDecorator> elemento é responsável por desenhar uma <xref:System.Windows.Controls.Button>borda e um fundo para o . O <xref:System.Windows.Controls.ContentPresenter> elemento é responsável por exibir <xref:System.Windows.Controls.Button>o conteúdo do . Neste caso, uma vez que você <xref:System.Windows.Controls.ContentPresenter> está <xref:System.Windows.Controls.TextBlock> exibindo texto, o elemento contém um elemento. O fato <xref:System.Windows.Controls.Button> de o <xref:System.Windows.Controls.ContentPresenter> controle usar um meio que o conteúdo <xref:System.Windows.Controls.Image> poderia ser representado por <xref:System.Windows.Media.EllipseGeometry>outros elementos, como uma ou uma geometria, como um .  
  
### <a name="control-templates"></a>Modelos de controle  
 A chave para a expansão de um controle <xref:System.Windows.Controls.ControlTemplate>em uma hierarquia de controles é o . Um modelo de controle especifica a hierarquia visual de um controle. Quando você referencia um controle explicitamente, você referencia implicitamente sua hierarquia visual. Você pode substituir os valores padrão de um modelo de controle para criar uma aparência visual personalizada para um controle. Por exemplo, você pode modificar o <xref:System.Windows.Controls.Button> valor de cor de fundo do controle para que ele use um valor de cor gradiente linear em vez de um valor de cor sólido. Para obter mais informações, consulte [Estilos e modelos de botão](../controls/button-styles-and-templates.md).  
  
 Um elemento de interface <xref:System.Windows.Controls.Button> de usuário, como um controle, contém várias listas de instruções de gráficos vetoriais que descrevem toda a definição de renderização de um controle. O código a <xref:System.Windows.Controls.Button> seguir mostra um controle definido na marcação.  
  
 [!code-xaml[VisualsOverview#VisualsOverviewSnippet2](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualsOverview/CSharp/Window1.xaml#visualsoverviewsnippet2)]  
  
 Se você enumerar os objetos visuais e as <xref:System.Windows.Controls.Button> listas de instruções de gráficos vetoriais que compõem o controle, você encontraria a hierarquia de objetos ilustrada abaixo:  
  
 ![Diagrama de árvore visual e dados de renderização](./media/wpf-graphics-rendering-overview/visual-tree-rendering-data.png)  
  
 O <xref:System.Windows.Controls.Button> controle <xref:Microsoft.Windows.Themes.ClassicBorderDecorator> contém um elemento, que <xref:System.Windows.Controls.ContentPresenter> por sua vez, contém um elemento. O <xref:Microsoft.Windows.Themes.ClassicBorderDecorator> elemento é responsável por desenhar todos os elementos gráficos discretos que compõem a borda e o fundo de um botão. O <xref:System.Windows.Controls.ContentPresenter> elemento é responsável por exibir <xref:System.Windows.Controls.Button>o conteúdo do . Neste caso, uma vez que você <xref:System.Windows.Controls.ContentPresenter> está exibindo <xref:System.Windows.Controls.Image> uma imagem, o elemento contém um elemento.  
  
 Há diversos pontos a observar sobre a hierarquia de objetos visuais e listas de instruções de gráficos vetoriais:  
  
- A ordem na hierarquia representa a ordem de renderização das informações de desenho. Do elemento visual raiz, a ordem de renderização passa pelos elementos filho da esquerda para a direita, de cima para baixo. Se um determinado elemento tem elementos visuais filho, a ordem de renderização passa por eles antes de passar pelos irmãos desse elemento.  
  
- Elementos de nó não folha na <xref:System.Windows.Controls.ContentPresenter>hierarquia, como , são usados para conter elementos de criança - eles não contêm listas de instruções.  
  
- Se um elemento visual contém uma lista de instruções de gráfico vetorial e filhos visuais, a lista de instruções no elemento visual pai é renderizada antes de desenhos em qualquer um dos objetos filho visuais.  
  
- Os itens na lista de instruções de gráficos vetoriais são renderizados da esquerda para a direita.  
  
<a name="visual_tree"></a>
## <a name="visual-tree"></a>Árvore visual  
 A árvore visual contém todos os elementos visuais usados na interface do usuário de um aplicativo. Já que um elemento visual contém informações de desenho persistentes, você pode pensar na árvore visual como um grafo de cena, contendo todas as informações de renderização necessárias para compor a saída para o dispositivo de vídeo. Esta árvore é o acúmulo de todos os elementos visuais criados diretamente pelo aplicativo, seja no código ou em marcação. A árvore visual também contém todos os elementos visuais criados pela expansão de modelo de elementos tais como controles e objetos de dados.  
  
 O código a <xref:System.Windows.Controls.StackPanel> seguir mostra um elemento definido na marcação.  
  
 [!code-xaml[VisualsOverview#VisualsOverviewSnippet3](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualsOverview/CSharp/Window1.xaml#visualsoverviewsnippet3)]  
  
 Se você enumerar os objetos <xref:System.Windows.Controls.StackPanel> visuais que compõem o elemento no exemplo de marcação, você encontraria a hierarquia de objetos visuais ilustrada abaixo:  
  
 ![Diagrama de hierarquia de árvore visual](./media/wpf-graphics-rendering-overview/visual-tree-hierarchy.gif)  
  
### <a name="rendering-order"></a>Ordem de renderização  
 A árvore visual determina a ordem de renderização de objetos visuais e de desenho do [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]. A ordem de passagem inicia com o visual raiz, que é o nó mais alto na árvore visual. Em seguida, passa-se pelos filhos do visual raiz, da esquerda para a direita. Se um visual tiver filhos, a passagem por eles ocorrerá primeiro do que a passagem pelos irmãos do visual. Isso significa que o conteúdo de um visual filho é renderizado na frente do conteúdo do próprio visual.  
  
 ![Diagrama da ordem de renderização da árvore visual](./media/wpf-graphics-rendering-overview/visual-tree-rendering-order.gif)
  
### <a name="root-visual"></a>Visual raiz  
 O **visual raiz** é o elemento mais alto em uma hierarquia de árvore visual. Na maioria das aplicações, a classe base <xref:System.Windows.Window> <xref:System.Windows.Navigation.NavigationWindow>do visual raiz é ou . No entanto, se você estivesse hospedando objetos visuais em um aplicativo Win32, o visual raiz seria o visual mais alto que você estivesse hospedando na janela Win32. Para obter mais informações, consulte [Tutorial: hospedando objetos visuais em um aplicativo Win32](tutorial-hosting-visual-objects-in-a-win32-application.md).  
  
### <a name="relationship-to-the-logical-tree"></a>Relacionamento com a árvore lógica  
 A árvore lógica no [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] representa os elementos de um aplicativo em tempo de execução. Embora você não manipule esta árvore diretamente, essa exibição do aplicativo é útil para entender a herança de propriedades e o roteamento de eventos. Ao contrário da árvore visual, a árvore lógica pode <xref:System.Windows.Documents.ListItem>representar objetos de dados não visuais, tais como . Em muitos casos, a árvore lógica mapeia de modo muito próximo às definições de marcação de um aplicativo. O código a <xref:System.Windows.Controls.DockPanel> seguir mostra um elemento definido na marcação.  
  
 [!code-xaml[VisualsOverview#VisualsOverviewSnippet5](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualsOverview/CSharp/Window1.xaml#visualsoverviewsnippet5)]  
  
 Se você enumerar os objetos <xref:System.Windows.Controls.DockPanel> lógicos que compõem o elemento no exemplo de marcação, você encontraria a hierarquia de objetos lógicos ilustradas abaixo:  
  
 ![Diagrama de árvore](./media/tree1-wcp.gif "Tree1_wcp")  
Diagrama de árvore lógica  
  
 A árvore visual e a árvore lógica são sincronizadas com o conjunto atual de elementos do aplicativo, refletindo qualquer adição, exclusão ou modificação de elementos. No entanto, as árvores apresentam diferentes exibições do aplicativo. Ao contrário da árvore visual, a árvore <xref:System.Windows.Controls.ContentPresenter> lógica não expande o elemento de um controle. Isso significa que não há uma correspondência um para um direta entre uma árvore lógica e uma árvore visual para o mesmo conjunto de objetos. Na verdade, invocar o método do <xref:System.Windows.LogicalTreeHelper.GetChildren%2A> objeto **LogicalTreeHelper** e o <xref:System.Windows.Media.VisualTreeHelper.GetChild%2A> método do objeto **VisualTreeHelper** usando o mesmo elemento que um parâmetro produz resultados diferentes.  
  
 Para obter mais informações sobre a árvore lógica, consulte [Árvores no WPF](../advanced/trees-in-wpf.md).  
  
### <a name="viewing-the-visual-tree-with-xamlpad"></a>Exibindo a árvore visual com XamlPad  
 A [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ferramenta, XamlPad, oferece uma opção para visualizar e explorar a árvore visual que corresponde ao conteúdo XAML atualmente definido. Clique no botão **Mostrar Árvore Visual** na barra de menus para exibir a árvore visual. O seguinte ilustra a expansão do conteúdo XAML em nós de árvore visuais no painel **Visual Tree Explorer** do XamlPad:  
  
 ![Painel Gerenciador de Árvore Visual no XamlPad](./media/wpf-graphics-rendering-overview/visual-tree-explorer.png)  

 Observe como <xref:System.Windows.Controls.Label> <xref:System.Windows.Controls.TextBox>o <xref:System.Windows.Controls.Button> , e controla cada um exibir uma hierarquia de objeto visual separado no painel **Visual Tree Explorer** do XamlPad. Isso porque [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] os controles <xref:System.Windows.Controls.ControlTemplate> têm uma árvore visual desse controle. Quando você referencia um controle explicitamente, você referencia implicitamente sua hierarquia visual.  
  
### <a name="profiling-visual-performance"></a>Criação de perfil de desempenho Visual  
 O [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] fornece um pacote de ferramentas de criação de perfil de desempenho que permitem analisar o comportamento de tempo de execução do aplicativo e determinar os tipos de otimização de desempenho que você pode aplicar. A ferramenta Visual Profiler fornece uma exibição gráfica sofisticada de dados de desempenho, por meio do mapeamento diretamente para a árvore visual do aplicativo. Nessa tela, a seção **Uso de CPU** do Visual Profiler lhe dá um detalhamento preciso do uso de um objeto de serviços do [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], assim como renderização e layout.  
  
 ![Saída de exibição do Visual Profiler](./media/wpfperf-visualprofiler-04.png "WPFPerf_VisualProfiler_04")  
Saída de exibição do Visual Profiler  
  
<a name="visual_rendering_behavior"></a>
## <a name="visual-rendering-behavior"></a>Comportamento de renderização visual  
 O [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] introduz diversos recursos que afetam o comportamento de renderização de objetos visuais: gráficos de modo retido, gráficos vetoriais e gráficos independentes de dispositivo.  
  
### <a name="retained-mode-graphics"></a>Gráficos de modo retido  
 Uma das chaves para entender o papel do objeto Visual é entender a diferença entre sistemas gráficos de **modo imediato** e de **modo retido**. Um aplicativo Win32 padrão baseado em GDI ou GDI+ utiliza um sistema gráfico de modo imediato. Isso significa que o aplicativo é responsável por repintar a parte da área de cliente que for invalidada, devido a uma ação como um redimensionamento de janela ou a alteração da aparência visual de um objeto.  
  
 ![Diagrama de sequência de renderização Win32](./media/wpf-graphics-rendering-overview/win32-rendering-squence.png)  
  
 Por outro lado, [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] usa um sistema de modo retido. Isso significa que os objetos de aplicativo que têm uma aparência visual definem um conjunto de dados de desenho serializados. A partir do momento em que os dados de desenho são definidos, o sistema torna-se responsável por responder a todas as solicitações de repintura para renderizar os objetos de aplicativo. Mesmo em tempo de execução, você pode modificar ou criar objetos de aplicativo e, ainda assim, contar com o sistema para responder às solicitações e pintura. O poder existente em um sistema gráfico de modo retido é que informações de desenho sempre são persistentes em um estado serializado pelo aplicativo, mas a responsabilidade pela renderização é deixada para o sistema. O diagrama a seguir mostra como o aplicativo depende do [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] para responder a solicitações de pintura.  
  
 ![Diagrama de sequência de renderização do WPF](./media/wpf-graphics-rendering-overview/wpf-rendering-sequence.png)  

#### <a name="intelligent-redrawing"></a>Redesenho inteligente  
 Um dos maiores benefícios de usar gráficos de modo retido é que o [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] pode otimizar de forma eficiente o que precisa ser redesenhado no aplicativo. Mesmo que você tenha uma cena complexa com diversos níveis de opacidade, você geralmente não precisa escrever código com propósito especial para otimizar o redesenho. Compare isso com programação em Win32, na qual você pode despender uma grande quantidade de esforço para otimizar seu aplicativo por meio da minimização da quantidade de redesenho na região de atualização. Consulte [Redesenho na região de atualização](/windows/desktop/gdi/redrawing-in-the-update-region) para obter um exemplo do tipo de complexidade envolvida na otimização de redesenho em aplicativos Win32.  
  
### <a name="vector-graphics"></a>Gráficos vetoriais  
 O [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] usa **gráficos vetoriais** como seu formato de dados de renderização. Gráficos vetoriais – que incluem SVG (Scalable Vector Graphics), metarquivos do Windows (.wmf) e fontes TrueType – armazenam dados de renderização e transmitem-nos como uma lista de instruções que descrevem como recriar uma imagem usando primitivos gráficos. Por exemplo, fontes TrueType são fontes geométricas que descrevem um conjunto de linhas, curvas e comandos, em vez de uma matriz de pixels. Um dos principais benefícios dos gráficos vetoriais é a capacidade de dimensionar para qualquer tamanho e resolução.  
  
 Diferente de gráficos vetoriais, gráficos de bitmap armazenam dados de renderização como uma representação pixel por pixel de uma imagem, pré-renderizada para uma determinada resolução. Uma das principais diferenças entre formatos de gráficos de bitmap e vetoriais é a fidelidade à imagem original. Por exemplo, quando o tamanho de uma imagem de origem é modificado, sistemas de gráficos de bitmap alongam a imagem, ao passo que sistemas de gráficos vetoriais redimensionam a imagem, preservando sua fidelidade.  
  
 A ilustração a seguir mostra uma imagem original que foi redimensionada em 300%. Observe as distorções que aparecem quando a imagem original é alongada como uma imagem de bitmap em vez de uma imagem de gráficos vetoriais.  
  
 ![Diferenças entre grafos rasterizados e vetoriais](./media/wpf-graphics-rendering-overview/raster-vector-differences.png)  
  
 A marcação a <xref:System.Windows.Shapes.Path> seguir mostra dois elementos definidos. O segundo elemento <xref:System.Windows.Media.ScaleTransform> usa um para redimensionar as instruções de desenho do primeiro elemento em 300%. Observe que as instruções de desenho nos <xref:System.Windows.Shapes.Path> elementos permanecem inalteradas.  
  
 [!code-xaml[VectorGraphicsSnippets#VectorGraphicsSnippet1](~/samples/snippets/csharp/VS_Snippets_Wpf/VectorGraphicsSnippets/CS/PageOne.xaml#vectorgraphicssnippet1)]  
  
### <a name="about-resolution-and-device-independent-graphics"></a>Sobre elementos gráficos independentes de resolução e de dispositivo  
 Há dois fatores de sistema que determinam o tamanho do texto e de elementos gráficos na sua tela: resolução e DPI. A resolução descreve o número de pixels que aparecem na tela. Conforme a resolução aumenta, os pixels ficam menores, fazendo com que elementos gráficos e texto apareçam menores. Um elemento gráfico exibido em um monitor definido para 1024 x 768 aparecerá bem menor quando a resolução for alterada para 1600 x 1200.  
  
 A configuração de sistema, DPI, descreve o tamanho de uma polegada de tela em pixels. A maioria dos sistemas Windows tem um DPI de 96, o que significa que uma polegada de tela é de 96 pixels. Aumentar a configuração de DPI torna a polegada de tela maior; diminuir o DPI torna a polegada de tela menor. Isso significa que uma polegada de tela não é do mesmo tamanho que uma polegada real; na maioria dos sistemas, provavelmente não é. Conforme você aumenta o DPI, texto e gráficos com reconhecimento de DPI se tornam maiores porque você aumentou o tamanho da polegada de tela. Aumentar o DPI pode tornar o texto mais fácil de ler, especialmente em resoluções altas.  
  
 Nem todos os aplicativos realizam reconhecimento de DPI: alguns utilizam pixels de hardware como a unidade principal de medida; alterar o DPI do sistema não tem nenhum efeito nesses aplicativos. Muitos outros aplicativos usam unidades com reconhecimento de DPI para descrever os tamanhos da fonte, mas utilizam pixels para descrever todo o resto. Tornar o DPI muito grande ou muito pequeno pode causar problemas de layout para esses aplicativos; o motivo disso é que o texto do aplicativo é dimensionado de acordo com a configuração de DPI do sistema, enquanto a interface do usuário não. Esse problema foi eliminado de aplicativos desenvolvidos usando o [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
 O [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] dá suporte ao dimensionamento automático usando o pixel independente de dispositivo como sua principal unidade de medida, em vez de pixels de hardware; texto e elementos gráficos são redimensionados adequadamente sem nenhum trabalho extra do desenvolvedor do aplicativo. A ilustração a seguir mostra um exemplo de como texto e elementos gráficos do [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] aparecem em diferentes configurações de DPI.  
  
 ![Elementos gráficos e texto em diferentes configurações de DPI](./media/graphicsmm-dpi-setting-examples.png "graphicsmm_dpi_setting_examples")  
Elementos gráficos e texto em diferentes configurações de DPI  
  
<a name="visualtreehelper_class"></a>
## <a name="visualtreehelper-class"></a>Classe VisualTreeHelper  
 A <xref:System.Windows.Media.VisualTreeHelper> classe é uma classe auxiliares estática que fornece funcionalidade de baixo nível para programação no nível do objeto visual, o que é útil em cenários muito específicos, como o desenvolvimento de controles personalizados de alto desempenho. Na maioria dos casos, [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] os objetos <xref:System.Windows.Controls.Canvas> <xref:System.Windows.Controls.TextBlock>de estrutura de nível superior, como e , oferecem maior flexibilidade e facilidade de uso.  
  
### <a name="hit-testing"></a>Testes de clique  
 A <xref:System.Windows.Media.VisualTreeHelper> classe fornece métodos para testes de acerto em objetos visuais quando o suporte padrão de teste de hit não atende às suas necessidades. Você pode <xref:System.Windows.Media.VisualTreeHelper.HitTest%2A> usar os <xref:System.Windows.Media.VisualTreeHelper> métodos da classe para determinar se uma geometria ou valor de coordenada de ponto está dentro do limite de um determinado objeto, como um controle ou elemento gráfico. Por exemplo, você pode usar o teste de clique para determinar se um clique do mouse dentro do retângulo delimitador de um objeto está dentro da geometria de um círculo. Você também pode optar por substituir a implementação padrão de teste de clique para executar seus próprios cálculos de teste de clique personalizados.  
  
 Para obter mais informações sobre teste de clique, consulte [Teste de clique na camada visual](hit-testing-in-the-visual-layer.md).  
  
### <a name="enumerating-the-visual-tree"></a>Enumerar a árvore Visual  
 A <xref:System.Windows.Media.VisualTreeHelper> classe oferece funcionalidade para enumerar os membros de uma árvore visual. Para recuperar um pai, ligue para o <xref:System.Windows.Media.VisualTreeHelper.GetParent%2A> método. Para recuperar uma criança, ou descendente direto, <xref:System.Windows.Media.VisualTreeHelper.GetChild%2A> de um objeto visual, chame o método. Este método retorna <xref:System.Windows.Media.Visual> um filho do pai no índice especificado.  
  
 O exemplo a seguir mostra como enumerar todos os descendentes de um objeto visual, que é uma técnica que talvez você queira usar caso esteja interessado em serializar a informação de renderização de uma hierarquia de objetos visuais.  
  
 [!code-csharp[VisualsOverview#101](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualsOverview/CSharp/Window1.xaml.cs#101)]
 [!code-vb[VisualsOverview#101](~/samples/snippets/visualbasic/VS_Snippets_Wpf/VisualsOverview/visualbasic/window1.xaml.vb#101)]  
  
 Na maioria dos casos, a árvore lógica é uma representação mais útil dos elementos em um aplicativo [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]. Embora você não modifique a árvore lógica diretamente, essa exibição do aplicativo é útil para entender a herança de propriedades e o roteamento de eventos. Ao contrário da árvore visual, a árvore lógica pode <xref:System.Windows.Documents.ListItem>representar objetos de dados não visuais, tais como . Para obter mais informações sobre a árvore lógica, consulte [Árvores no WPF](../advanced/trees-in-wpf.md).  
  
 A <xref:System.Windows.Media.VisualTreeHelper> classe fornece métodos para devolver o retângulo delimitador de objetos visuais. Você pode retornar o retângulo delimitador <xref:System.Windows.Media.VisualTreeHelper.GetContentBounds%2A>de um objeto visual chamando . Você pode retornar o retângulo delimitador de todos os descendentes de <xref:System.Windows.Media.VisualTreeHelper.GetDescendantBounds%2A>um objeto visual, incluindo o objeto visual em si, chamando . O código a seguir mostra como você calcularia o retângulo delimitador de um objeto visual e todos os seus descendentes.  
  
 [!code-csharp[VisualsOverview#102](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualsOverview/CSharp/Window1.xaml.cs#102)]
 [!code-vb[VisualsOverview#102](~/samples/snippets/visualbasic/VS_Snippets_Wpf/VisualsOverview/visualbasic/window1.xaml.vb#102)]  
  
## <a name="see-also"></a>Confira também

- <xref:System.Windows.Media.Visual>
- <xref:System.Windows.Media.VisualTreeHelper>
- <xref:System.Windows.Media.DrawingVisual>
- [Elementos gráficos e geração de imagens 2D](../advanced/optimizing-performance-2d-graphics-and-imaging.md)
- [Teste de clique na camada visual](hit-testing-in-the-visual-layer.md)
- [Usando objetos DrawingVisual](using-drawingvisual-objects.md)
- [Tutorial: hospedando objetos visuais em um aplicativo Win32](tutorial-hosting-visual-objects-in-a-win32-application.md)
- [Otimizando o desempenho do aplicativo WPF](../advanced/optimizing-wpf-application-performance.md)
