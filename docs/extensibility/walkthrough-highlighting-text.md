---
title: 'チュートリアル: テキストの強調表示 |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - highlight text
ms.assetid: 64b772ad-4392-42e9-a237-5137f0384bf0
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: dd19077424aa5f67cd1d3a8d7f9c6be0e822e351
ms.sourcegitcommit: 8e123bcb21279f2770b28696995450270b4ec0e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/25/2019
ms.locfileid: "75403592"
---
# <a name="walkthrough-highlight-text"></a>チュートリアル: テキストの強調表示
Managed Extensibility Framework (MEF) コンポーネントパーツを作成することによって、エディターにさまざまな視覚効果を追加できます。 このチュートリアルでは、テキストファイル内で現在の単語が出現するたびに強調表示する方法について説明します。 1つの単語がテキストファイル内に複数回出現し、カレットを1回の出現時に配置すると、すべての出現箇所が強調表示されます。

## <a name="prerequisites"></a>Prerequisites
 Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 また、後から VS SDK をインストールすることもできます。 詳細については、"[Visual Studio SDK をインストール](../extensibility/installing-the-visual-studio-sdk.md)"を参照してください。

## <a name="create-a-mef-project"></a>MEF プロジェクトを作成する

1. VSIX プロジェクトC#を作成します。 ( **[新しいプロジェクト]** ダイアログで、 **[ C#ビジュアル/機能拡張**]、 **[VSIX プロジェクト]** の順に選択します)。ソリューションに `HighlightWordTest`という名前を指定します。

2. エディター分類子項目テンプレートをプロジェクトに追加します。 詳細については、「[エディター項目テンプレートを使用して拡張機能を作成](../extensibility/creating-an-extension-with-an-editor-item-template.md)する」を参照してください。

3. 既存のクラス ファイルを削除します。

## <a name="define-a-textmarkertag"></a>TextMarkerTag を定義する
 テキストを強調表示する最初の手順は、<xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag> をサブクラス化し、その外観を定義することです。

### <a name="to-define-a-textmarkertag-and-a-markerformatdefinition"></a>TextMarkerTag と MarkerFormatDefinition を定義するには

1. クラスファイルを追加し、 **HighlightWordTag**という名前を指定します。

2. 次の参照を追加します。

    1. Microsoft.VisualStudio.CoreUtility

    2. VisualStudio のデータ

    3. Microsoft.VisualStudio.Text.Logic

    4. VisualStudio. UI

    5. VisualStudio (Microsoft. UI)

    6. System.ComponentModel.Composition

    7. プレゼンテーション。コア

    8. Presentation. Framework

3. 次の名前空間をインポートします。

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.ComponentModel.Composition;
    using System.Linq;
    using System.Threading;
    using Microsoft.VisualStudio.Text;
    using Microsoft.VisualStudio.Text.Classification;
    using Microsoft.VisualStudio.Text.Editor;
    using Microsoft.VisualStudio.Text.Operations;
    using Microsoft.VisualStudio.Text.Tagging;
    using Microsoft.VisualStudio.Utilities;
    using System.Windows.Media;
    ```

4. <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag> から継承するクラスを作成し、`HighlightWordTag`という名前を指定します。

    ```csharp
    internal class HighlightWordTag : TextMarkerTag
    {

    }
    ```

5. <xref:Microsoft.VisualStudio.Text.Classification.MarkerFormatDefinition>から継承する2番目のクラスを作成し、`HighlightWordFormatDefinition`という名前を指定します。 タグにこの形式定義を使用するには、次の属性を使用してエクスポートする必要があります。

    - <xref:Microsoft.VisualStudio.Utilities.NameAttribute>: タグはこの形式を参照するために使用します

    - <xref:Microsoft.VisualStudio.Text.Classification.UserVisibleAttribute>: これにより、形式が UI に表示されます。

    ```csharp

    [Export(typeof(EditorFormatDefinition))]
    [Name("MarkerFormatDefinition/HighlightWordFormatDefinition")]
    [UserVisible(true)]
    internal class HighlightWordFormatDefinition : MarkerFormatDefinition
    {

    }
    ```

6. HighlightWordFormatDefinition のコンストラクターで、表示名と外観を定義します。 Background プロパティは塗りつぶしの色を定義し、前景プロパティは境界線の色を定義します。

    ```csharp
    public HighlightWordFormatDefinition()
    {
                this.BackgroundColor = Colors.LightBlue;
        this.ForegroundColor = Colors.DarkBlue;
        this.DisplayName = "Highlight Word";
        this.ZOrder = 5;
    }
    ```

7. HighlightWordTag のコンストラクターで、作成した書式定義の名前を渡します。

    ```
    public HighlightWordTag() : base("MarkerFormatDefinition/HighlightWordFormatDefinition") { }
    ```

## <a name="implement-an-itagger"></a>ITagger を実装する
 次の手順では、<xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601> インターフェイスを実装します。 このインターフェイスは、特定のテキストバッファーに、テキストの強調表示やその他の視覚効果を提供するタグを割り当てます。

### <a name="to-implement-a-tagger"></a>タガーを実装するには

1. `HighlightWordTag`型の <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601> を実装するクラスを作成し、`HighlightWordTagger`という名前を指定します。

    ```csharp
    internal class HighlightWordTagger : ITagger<HighlightWordTag>
    {

    }
    ```

2. 次のプライベートフィールドとプロパティをクラスに追加します。

    - 現在のテキストビューに対応する <xref:Microsoft.VisualStudio.Text.Editor.ITextView>。

    - テキストビューの基になるテキストバッファーに対応する <xref:Microsoft.VisualStudio.Text.ITextBuffer>。

    - テキストを検索するために使用される <xref:Microsoft.VisualStudio.Text.Operations.ITextSearchService>。

    - <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigator>。テキスト範囲内を移動するためのメソッドがあります。

    - 強調表示する単語のセットを含む <xref:Microsoft.VisualStudio.Text.NormalizedSnapshotSpanCollection>。

    - 現在の単語に対応する <xref:Microsoft.VisualStudio.Text.SnapshotSpan>。

    - キャレットの現在位置に対応する <xref:Microsoft.VisualStudio.Text.SnapshotPoint>。

    - ロックオブジェクト。

    ```csharp
    ITextView View { get; set; }
    ITextBuffer SourceBuffer { get; set; }
    ITextSearchService TextSearchService { get; set; }
    ITextStructureNavigator TextStructureNavigator { get; set; }
    NormalizedSnapshotSpanCollection WordSpans { get; set; }
    SnapshotSpan? CurrentWord { get; set; }
    SnapshotPoint RequestedPoint { get; set; }
    object updateLock = new object();

    ```

3. 前に示したプロパティを初期化するコンストラクターを追加し、<xref:Microsoft.VisualStudio.Text.Editor.ITextView.LayoutChanged> および <xref:Microsoft.VisualStudio.Text.Editor.ITextCaret.PositionChanged> のイベントハンドラーを追加します。

    ```csharp
    public HighlightWordTagger(ITextView view, ITextBuffer sourceBuffer, ITextSearchService textSearchService,
    ITextStructureNavigator textStructureNavigator)
    {
        this.View = view;
        this.SourceBuffer = sourceBuffer;
        this.TextSearchService = textSearchService;
        this.TextStructureNavigator = textStructureNavigator;
        this.WordSpans = new NormalizedSnapshotSpanCollection();
        this.CurrentWord = null;
        this.View.Caret.PositionChanged += CaretPositionChanged;
        this.View.LayoutChanged += ViewLayoutChanged;
    }

    ```

4. イベントハンドラーはどちらも `UpdateAtCaretPosition` メソッドを呼び出します。

    ```csharp
    void ViewLayoutChanged(object sender, TextViewLayoutChangedEventArgs e)
    {
        // If a new snapshot wasn't generated, then skip this layout 
        if (e.NewSnapshot != e.OldSnapshot)
        {
            UpdateAtCaretPosition(View.Caret.Position);
        }
    }

    void CaretPositionChanged(object sender, CaretPositionChangedEventArgs e)
    {
        UpdateAtCaretPosition(e.NewPosition);
    }
    ```

5. また、update メソッドによって呼び出される `TagsChanged` イベントも追加する必要があります。

     [!code-csharp[VSSDKHighlightWordTest#10](../extensibility/codesnippet/CSharp/walkthrough-highlighting-text_1.cs)]
     [!code-vb[VSSDKHighlightWordTest#10](../extensibility/codesnippet/VisualBasic/walkthrough-highlighting-text_1.vb)]

6. `UpdateAtCaretPosition()` メソッドは、テキストバッファー内のすべての単語を、カーソルが置かれている単語と同一で検索し、その単語の出現に対応する <xref:Microsoft.VisualStudio.Text.SnapshotSpan> オブジェクトの一覧を構築します。 次に、`SynchronousUpdate`を呼び出します。これにより、`TagsChanged` イベントが発生します。

    ```csharp
    void UpdateAtCaretPosition(CaretPosition caretPosition)
    {
        SnapshotPoint? point = caretPosition.Point.GetPoint(SourceBuffer, caretPosition.Affinity);

        if (!point.HasValue)
            return;

        // If the new caret position is still within the current word (and on the same snapshot), we don't need to check it 
        if (CurrentWord.HasValue
            && CurrentWord.Value.Snapshot == View.TextSnapshot
            && point.Value >= CurrentWord.Value.Start
            && point.Value <= CurrentWord.Value.End)
        {
            return;
        }

        RequestedPoint = point.Value;
        UpdateWordAdornments();
    }

    void UpdateWordAdornments()
    {
        SnapshotPoint currentRequest = RequestedPoint;
        List<SnapshotSpan> wordSpans = new List<SnapshotSpan>();
        //Find all words in the buffer like the one the caret is on
        TextExtent word = TextStructureNavigator.GetExtentOfWord(currentRequest);
        bool foundWord = true;
        //If we've selected something not worth highlighting, we might have missed a "word" by a little bit
        if (!WordExtentIsValid(currentRequest, word))
        {
            //Before we retry, make sure it is worthwhile 
            if (word.Span.Start != currentRequest
                 || currentRequest == currentRequest.GetContainingLine().Start
                 || char.IsWhiteSpace((currentRequest - 1).GetChar()))
            {
                foundWord = false;
            }
            else
            {
                // Try again, one character previous.  
                //If the caret is at the end of a word, pick up the word.
                word = TextStructureNavigator.GetExtentOfWord(currentRequest - 1);

                //If the word still isn't valid, we're done 
                if (!WordExtentIsValid(currentRequest, word))
                    foundWord = false;
            }
        }

        if (!foundWord)
        {
            //If we couldn't find a word, clear out the existing markers
            SynchronousUpdate(currentRequest, new NormalizedSnapshotSpanCollection(), null);
            return;
        }

        SnapshotSpan currentWord = word.Span;
        //If this is the current word, and the caret moved within a word, we're done. 
        if (CurrentWord.HasValue && currentWord == CurrentWord)
            return;

        //Find the new spans
        FindData findData = new FindData(currentWord.GetText(), currentWord.Snapshot);
        findData.FindOptions = FindOptions.WholeWord | FindOptions.MatchCase;

        wordSpans.AddRange(TextSearchService.FindAll(findData));

        //If another change hasn't happened, do a real update 
        if (currentRequest == RequestedPoint)
            SynchronousUpdate(currentRequest, new NormalizedSnapshotSpanCollection(wordSpans), currentWord);
    }
    static bool WordExtentIsValid(SnapshotPoint currentRequest, TextExtent word)
    {
        return word.IsSignificant
            && currentRequest.Snapshot.GetText(word.Span).Any(c => char.IsLetter(c));
    }

    ```

7. `SynchronousUpdate` によって `WordSpans` と `CurrentWord` のプロパティに対して同期更新が実行され、`TagsChanged` イベントが発生します。

    ```csharp
    void SynchronousUpdate(SnapshotPoint currentRequest, NormalizedSnapshotSpanCollection newSpans, SnapshotSpan? newCurrentWord)
    {
        lock (updateLock)
        {
            if (currentRequest != RequestedPoint)
                return;

            WordSpans = newSpans;
            CurrentWord = newCurrentWord;

            var tempEvent = TagsChanged;
            if (tempEvent != null)
                tempEvent(this, new SnapshotSpanEventArgs(new SnapshotSpan(SourceBuffer.CurrentSnapshot, 0, SourceBuffer.CurrentSnapshot.Length)));
        }
    }
    ```

8. <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601.GetTags%2A> メソッドを実装する必要があります。 このメソッドは <xref:Microsoft.VisualStudio.Text.SnapshotSpan> オブジェクトのコレクションを受け取り、タグ範囲の列挙体を返します。

     でC#は、このメソッドを yield 反復子として実装します。これにより、タグの遅延評価 (つまり、個々の項目にアクセスしたときにのみ、セットの評価) が有効になります。 Visual Basic で、タグを一覧に追加し、一覧を返します。

     ここで、メソッドは、青い背景を提供する "blue" <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag>を持つ <xref:Microsoft.VisualStudio.Text.Tagging.TagSpan%601> オブジェクトを返します。

    ```csharp
    public IEnumerable<ITagSpan<HighlightWordTag>> GetTags(NormalizedSnapshotSpanCollection spans)
    {
        if (CurrentWord == null)
            yield break;

        // Hold on to a "snapshot" of the word spans and current word, so that we maintain the same
        // collection throughout
        SnapshotSpan currentWord = CurrentWord.Value;
        NormalizedSnapshotSpanCollection wordSpans = WordSpans;

        if (spans.Count == 0 || wordSpans.Count == 0)
            yield break;

        // If the requested snapshot isn't the same as the one our words are on, translate our spans to the expected snapshot 
        if (spans[0].Snapshot != wordSpans[0].Snapshot)
        {
            wordSpans = new NormalizedSnapshotSpanCollection(
                wordSpans.Select(span => span.TranslateTo(spans[0].Snapshot, SpanTrackingMode.EdgeExclusive)));

            currentWord = currentWord.TranslateTo(spans[0].Snapshot, SpanTrackingMode.EdgeExclusive);
        }

        // First, yield back the word the cursor is under (if it overlaps) 
        // Note that we'll yield back the same word again in the wordspans collection; 
        // the duplication here is expected. 
        if (spans.OverlapsWith(new NormalizedSnapshotSpanCollection(currentWord)))
            yield return new TagSpan<HighlightWordTag>(currentWord, new HighlightWordTag());

        // Second, yield all the other words in the file 
        foreach (SnapshotSpan span in NormalizedSnapshotSpanCollection.Overlap(spans, wordSpans))
        {
            yield return new TagSpan<HighlightWordTag>(span, new HighlightWordTag());
        }
    }
    ```

## <a name="create-a-tagger-provider"></a>Tagger プロバイダーを作成する
 タグを作成するには、<xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider>を実装する必要があります。 このクラスは MEF コンポーネント部分なので、この拡張機能が認識されるように、正しい属性を設定する必要があります。

> [!NOTE]
> MEF の詳細については、「 [Managed Extensibility Framework (mef)](/dotnet/framework/mef/index)」を参照してください。

### <a name="to-create-a-tagger-provider"></a>タガープロバイダーを作成するには

1. <xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider>を実装する `HighlightWordTaggerProvider` という名前のクラスを作成し、"text" の <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> および <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag>の <xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute> を使用してエクスポートします。

    ```csharp
    [Export(typeof(IViewTaggerProvider))]
    [ContentType("text")]
    [TagType(typeof(TextMarkerTag))]
    internal class HighlightWordTaggerProvider : IViewTaggerProvider
    { }
    ```

2. タグをインスタンス化するには、2つのエディターサービス (<xref:Microsoft.VisualStudio.Text.Operations.ITextSearchService> と <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService>) をインポートする必要があります。

    ```csharp
    [Import]
    internal ITextSearchService TextSearchService { get; set; }

    [Import]
    internal ITextStructureNavigatorSelectorService TextStructureNavigatorSelector { get; set; }

    ```

3. `HighlightWordTagger`のインスタンスを返すには、<xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider.CreateTagger%2A> メソッドを実装します。

    ```csharp
    public ITagger<T> CreateTagger<T>(ITextView textView, ITextBuffer buffer) where T : ITag
    {
        //provide highlighting only on the top buffer 
        if (textView.TextBuffer != buffer)
            return null;

        ITextStructureNavigator textStructureNavigator =
            TextStructureNavigatorSelector.GetTextStructureNavigator(buffer);

        return new HighlightWordTagger(textView, buffer, TextSearchService, textStructureNavigator) as ITagger<T>;
    }
    ```

## <a name="build-and-test-the-code"></a>コードをビルドしてテストする
 このコードをテストするには、HighlightWordTest ソリューションをビルドし、実験用インスタンスで実行します。

### <a name="to-build-and-test-the-highlightwordtest-solution"></a>HighlightWordTest ソリューションをビルドしてテストするには

1. ソリューションをビルドします。

2. デバッガーでこのプロジェクトを実行すると、Visual Studio の2番目のインスタンスが開始されます。

3. テキストファイルを作成し、単語が繰り返されるいくつかのテキストを入力します ("hello hello hello" など)。

4. "Hello" のいずれかの位置にカーソルを置きます。 すべての出現箇所が青色で強調表示されます。

## <a name="see-also"></a>関連項目
- [チュートリアル: コンテンツの種類をファイル名拡張子にリンクする](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)
