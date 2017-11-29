---
title: Expressions de calcul (F#)
description: "Découvrez comment créer la syntaxe pour l’écriture de calculs en F # qui peuvent être séquencés et combinés à l’aide de liaisons et constructions de flux de contrôle."
keywords: visual f#, f#, programmation fonctionnelle
author: cartermp
ms.author: phcart
ms.date: 05/16/2016
ms.topic: language-reference
ms.prod: .net
ms.technology: devlang-fsharp
ms.devlang: fsharp
ms.assetid: acabbf5d-fbb8-479f-894c-7251bf16c8c3
ms.openlocfilehash: 15ba2e167efc1d295d81439dcf85bc7272e05265
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/18/2017
---
# <a name="computation-expressions"></a><span data-ttu-id="89943-104">Expressions de calcul</span><span class="sxs-lookup"><span data-stu-id="89943-104">Computation Expressions</span></span>

<span data-ttu-id="89943-105">En F #, les expressions de calcul fournissent une syntaxe pratique pour l’écriture de calculs qui peuvent être séquencés et combinés à l’aide de liaisons et constructions de flux de contrôle.</span><span class="sxs-lookup"><span data-stu-id="89943-105">Computation expressions in F# provide a convenient syntax for writing computations that can be sequenced and combined using control flow constructs and bindings.</span></span> <span data-ttu-id="89943-106">Elles peuvent servir à fournir une syntaxe pratique pour *monades*, une fonctionnalité de programmation fonctionnelle qui peut être utilisée pour gérer les données, le contrôle et les effets secondaires dans les programmes fonctionnels.</span><span class="sxs-lookup"><span data-stu-id="89943-106">They can be used to provide a convenient syntax for *monads*, a functional programming feature that can be used to manage data, control, and side effects in functional programs.</span></span>


## <a name="built-in-workflows"></a><span data-ttu-id="89943-107">Flux de travail intégrés</span><span class="sxs-lookup"><span data-stu-id="89943-107">Built-in Workflows</span></span>
<span data-ttu-id="89943-108">Expressions de séquence sont un exemple d’expression de calcul, comme les flux de travail asynchrones et les expressions de requête.</span><span class="sxs-lookup"><span data-stu-id="89943-108">Sequence expressions are an example of a computation expression, as are asynchronous workflows and query expressions.</span></span> <span data-ttu-id="89943-109">Pour plus d’informations, consultez [séquences](sequences.md), [Workflows asynchrones](asynchronous-workflows.md), et [les Expressions de requête](query-expressions.md).</span><span class="sxs-lookup"><span data-stu-id="89943-109">For more information, see [Sequences](sequences.md), [Asynchronous Workflows](asynchronous-workflows.md), and [Query Expressions](query-expressions.md).</span></span>

<span data-ttu-id="89943-110">Certaines fonctionnalités communes aux expressions de séquence et flux de travail asynchrones et illustrent la syntaxe de base pour une expression de calcul :</span><span class="sxs-lookup"><span data-stu-id="89943-110">Certain features are common to both sequence expressions and asynchronous workflows and illustrate the basic syntax for a computation expression:</span></span>

```fsharp
builder-name { expression }
```

<span data-ttu-id="89943-111">La syntaxe précédente spécifie que l’expression donnée est une expression de calcul d’un type spécifié par *-nom du Générateur de*.</span><span class="sxs-lookup"><span data-stu-id="89943-111">The previous syntax specifies that the given expression is a computation expression of a type specified by *builder-name*.</span></span> <span data-ttu-id="89943-112">L’expression de calcul peut être un flux de travail intégré, tel que `seq` ou `async`, ou il peut être quelque chose que vous définissez.</span><span class="sxs-lookup"><span data-stu-id="89943-112">The computation expression can be a built-in workflow, such as `seq` or `async`, or it can be something you define.</span></span> <span data-ttu-id="89943-113">Le *-nom du Générateur de* est l’identificateur pour une instance d’un type spécial appelé le *type de générateur*.</span><span class="sxs-lookup"><span data-stu-id="89943-113">The *builder-name* is the identifier for an instance of a special type known as the *builder type*.</span></span> <span data-ttu-id="89943-114">Le type de générateur est un type de classe qui définit des méthodes spéciales qui régissent la façon des que fragments de l’expression de calcul sont combinées, autrement dit, code qui contrôle la façon dont l’expression s’exécute.</span><span class="sxs-lookup"><span data-stu-id="89943-114">The builder type is a class type that defines special methods that govern the way the fragments of the computation expression are combined, that is, code that controls how the expression executes.</span></span> <span data-ttu-id="89943-115">Une autre pour décrire une classe de générateur consiste à dire qu’il vous permet de personnaliser l’opération de nombreuses constructions F #, telles que les boucles et les liaisons.</span><span class="sxs-lookup"><span data-stu-id="89943-115">Another way to describe a builder class is to say that it enables you to customize the operation of many F# constructs, such as loops and bindings.</span></span>

<span data-ttu-id="89943-116">Dans les expressions de calcul, les deux formes sont disponibles pour certaines constructions de langage commun.</span><span class="sxs-lookup"><span data-stu-id="89943-116">In computation expressions, two forms are available for some common language constructs.</span></span> <span data-ttu-id="89943-117">Vous pouvez appeler les constructions de type variant en utilisant un !</span><span class="sxs-lookup"><span data-stu-id="89943-117">You can invoke the variant constructs by using a !</span></span> <span data-ttu-id="89943-118">(bang) sur certains mots clés, le suffixe tel que `let!`, `do!`, et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="89943-118">(bang) suffix on certain keywords, such as `let!`, `do!`, and so on.</span></span> <span data-ttu-id="89943-119">Ces formulaires spéciaux forcent certaines fonctions définies dans la classe de générateur à remplacer le comportement intégré ordinaire de ces opérations.</span><span class="sxs-lookup"><span data-stu-id="89943-119">These special forms cause certain functions defined in the builder class to replace the ordinary built-in behavior of these operations.</span></span> <span data-ttu-id="89943-120">Ces formes ressemblent à la `yield!` formulaire de la `yield` mot clé qui est utilisée dans les expressions de séquence.</span><span class="sxs-lookup"><span data-stu-id="89943-120">These forms resemble the `yield!` form of the `yield` keyword that is used in sequence expressions.</span></span> <span data-ttu-id="89943-121">Pour plus d’informations, consultez [séquences](sequences.md).</span><span class="sxs-lookup"><span data-stu-id="89943-121">For more information, see [Sequences](sequences.md).</span></span>


## <a name="creating-a-new-type-of-computation-expression"></a><span data-ttu-id="89943-122">Création d’un nouveau Type d’Expression de calcul</span><span class="sxs-lookup"><span data-stu-id="89943-122">Creating a New Type of Computation Expression</span></span>
<span data-ttu-id="89943-123">Vous pouvez définir les caractéristiques de vos propres expressions de calcul en créant une classe de générateur et en définissant certaines méthodes spéciales sur la classe.</span><span class="sxs-lookup"><span data-stu-id="89943-123">You can define the characteristics of your own computation expressions by creating a builder class and defining certain special methods on the class.</span></span> <span data-ttu-id="89943-124">La classe de générateur peut éventuellement définir les méthodes, comme indiqué dans le tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="89943-124">The builder class can optionally define the methods as listed in the following table.</span></span>

<span data-ttu-id="89943-125">Le tableau suivant décrit les méthodes qui peuvent être utilisées dans une classe de générateur de flux de travail.</span><span class="sxs-lookup"><span data-stu-id="89943-125">The following table describes methods that can be used in a workflow builder class.</span></span>


|<span data-ttu-id="89943-126">**Méthode**</span><span class="sxs-lookup"><span data-stu-id="89943-126">**Method**</span></span>|<span data-ttu-id="89943-127">**Typiques**</span><span class="sxs-lookup"><span data-stu-id="89943-127">**Typical signature(s)**</span></span>|<span data-ttu-id="89943-128">**Description**</span><span class="sxs-lookup"><span data-stu-id="89943-128">**Description**</span></span>|
|----|----|----|
|`Bind`|`M<'T> * ('T -> M<'U>) -> M<'U>`|<span data-ttu-id="89943-129">Appelé pour `let!` et `do!` dans les expressions de calcul.</span><span class="sxs-lookup"><span data-stu-id="89943-129">Called for `let!` and `do!` in computation expressions.</span></span>|
|`Delay`|`(unit -> M<'T>) -> M<'T>`|<span data-ttu-id="89943-130">Encapsule une expression de calcul en tant que fonction.</span><span class="sxs-lookup"><span data-stu-id="89943-130">Wraps a computation expression as a function.</span></span>|
|`Return`|`'T -> M<'T>`|<span data-ttu-id="89943-131">Appelé pour `return` dans les expressions de calcul.</span><span class="sxs-lookup"><span data-stu-id="89943-131">Called for `return` in computation expressions.</span></span>|
|`ReturnFrom`|`M<'T> -> M<'T>`|<span data-ttu-id="89943-132">Appelé pour `return!` dans les expressions de calcul.</span><span class="sxs-lookup"><span data-stu-id="89943-132">Called for `return!` in computation expressions.</span></span>|
|`Run`|<span data-ttu-id="89943-133">`M<'T> -> M<'T>` ou</span><span class="sxs-lookup"><span data-stu-id="89943-133">`M<'T> -> M<'T>` or</span></span><br /><br />`M<'T> -> 'T`|<span data-ttu-id="89943-134">Exécute une expression de calcul.</span><span class="sxs-lookup"><span data-stu-id="89943-134">Executes a computation expression.</span></span>|
|`Combine`|<span data-ttu-id="89943-135">`M<'T> * M<'T> -> M<'T>` ou</span><span class="sxs-lookup"><span data-stu-id="89943-135">`M<'T> * M<'T> -> M<'T>` or</span></span><br /><br />`M<unit> * M<'T> -> M<'T>`|<span data-ttu-id="89943-136">Appelée pour le séquencement dans les expressions de calcul.</span><span class="sxs-lookup"><span data-stu-id="89943-136">Called for sequencing in computation expressions.</span></span>|
|`For`|<span data-ttu-id="89943-137">`seq<'T> * ('T -> M<'U>) -> M<'U>` ou</span><span class="sxs-lookup"><span data-stu-id="89943-137">`seq<'T> * ('T -> M<'U>) -> M<'U>` or</span></span><br /><br />`seq<'T> * ('T -> M<'U>) -> seq<M<'U>>`|<span data-ttu-id="89943-138">Appelé pour `for...do` expressions dans les expressions de calcul.</span><span class="sxs-lookup"><span data-stu-id="89943-138">Called for `for...do` expressions in computation expressions.</span></span>|
|`TryFinally`|`M<'T> * (unit -> unit) -> M<'T>`|<span data-ttu-id="89943-139">Appelé pour `try...finally` expressions dans les expressions de calcul.</span><span class="sxs-lookup"><span data-stu-id="89943-139">Called for `try...finally` expressions in computation expressions.</span></span>|
|`TryWith`|`M<'T> * (exn -> M<'T>) -> M<'T>`|<span data-ttu-id="89943-140">Appelé pour `try...with` expressions dans les expressions de calcul.</span><span class="sxs-lookup"><span data-stu-id="89943-140">Called for `try...with` expressions in computation expressions.</span></span>|
|`Using`|`'T * ('T -> M<'U>) -> M<'U> when 'U :> IDisposable`|<span data-ttu-id="89943-141">Appelé pour `use` liaisons dans les expressions de calcul.</span><span class="sxs-lookup"><span data-stu-id="89943-141">Called for `use` bindings in computation expressions.</span></span>|
|`While`|`(unit -> bool) * M<'T> -> M<'T>`|<span data-ttu-id="89943-142">Appelé pour `while...do` expressions dans les expressions de calcul.</span><span class="sxs-lookup"><span data-stu-id="89943-142">Called for `while...do` expressions in computation expressions.</span></span>|
|`Yield`|`'T -> M<'T>`|<span data-ttu-id="89943-143">Appelé pour `yield` expressions dans les expressions de calcul.</span><span class="sxs-lookup"><span data-stu-id="89943-143">Called for `yield` expressions in computation expressions.</span></span>|
|`YieldFrom`|`M<'T> -> M<'T>`|<span data-ttu-id="89943-144">Appelé pour `yield!` expressions dans les expressions de calcul.</span><span class="sxs-lookup"><span data-stu-id="89943-144">Called for `yield!` expressions in computation expressions.</span></span>|
|`Zero`|`unit -> M<'T>`|<span data-ttu-id="89943-145">Appelé pour vide `else` branches de `if...then` expressions dans les expressions de calcul.</span><span class="sxs-lookup"><span data-stu-id="89943-145">Called for empty `else` branches of `if...then` expressions in computation expressions.</span></span>|
<span data-ttu-id="89943-146">La plupart des méthodes dans une classe de générateur utilisent et renvoyer un `M<'T>` construction, qui est généralement un type défini séparément qui caractérise le genre des calculs combinés, par exemple, `Async<'T>` pour les flux de travail asynchrones et `Seq<'T>` pour les workflows de la séquence.</span><span class="sxs-lookup"><span data-stu-id="89943-146">Many of the methods in a builder class use and return an `M<'T>` construct, which is typically a separately defined type that characterizes the kind of computations being combined, for example, `Async<'T>` for asynchronous workflows and `Seq<'T>` for sequence workflows.</span></span> <span data-ttu-id="89943-147">Les signatures de ces méthodes pouvoir être combinées et imbriquées avec d’autres, afin que l’objet de flux de travail retourné d’une construction permettre être passée à la suivante.</span><span class="sxs-lookup"><span data-stu-id="89943-147">The signatures of these methods enable them to be combined and nested with each other, so that the workflow object returned from one construct can be passed to the next.</span></span> <span data-ttu-id="89943-148">Le compilateur, lorsqu’il analyse une expression de calcul, convertit l’expression en une série d’appels de fonction imbriqués en utilisant les méthodes dans le tableau précédent et le code dans l’expression de calcul.</span><span class="sxs-lookup"><span data-stu-id="89943-148">The compiler, when it parses a computation expression, converts the expression into a series of nested function calls by using the methods in the preceding table and the code in the computation expression.</span></span>

<span data-ttu-id="89943-149">L’expression imbriquée a la forme suivante :</span><span class="sxs-lookup"><span data-stu-id="89943-149">The nested expression is of the following form:</span></span>

```fsharp
builder.Run(builder.Delay(fun () -> {| cexpr |}))
```

<span data-ttu-id="89943-150">Dans le code ci-dessus, les appels à `Run` et `Delay` sont omis s’ils ne sont pas définis dans la classe de générateur d’expression de calcul.</span><span class="sxs-lookup"><span data-stu-id="89943-150">In the above code, the calls to `Run` and `Delay` are omitted if they are not defined in the computation expression builder class.</span></span> <span data-ttu-id="89943-151">Le corps de l’expression de calcul, désignée ici comme `{| cexpr |}`, est traduite en appels de méthodes de la classe de générateur par les traductions décrites dans le tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="89943-151">The body of the computation expression, here denoted as `{| cexpr |}`, is translated into calls involving the methods of the builder class by the translations described in the following table.</span></span> <span data-ttu-id="89943-152">L’expression de calcul `{| cexpr |}` est définie de manière récursive en fonction de ces traductions où `expr` est une expression F # et `cexpr` est une expression de calcul.</span><span class="sxs-lookup"><span data-stu-id="89943-152">The computation expression `{| cexpr |}` is defined recursively according to these translations where `expr` is an F# expression and `cexpr` is a computation expression.</span></span>



|<span data-ttu-id="89943-153">Expression</span><span class="sxs-lookup"><span data-stu-id="89943-153">Expression</span></span>|<span data-ttu-id="89943-154">Traduction</span><span class="sxs-lookup"><span data-stu-id="89943-154">Translation</span></span>|
|----------|-----------|
|<code>{&#124; let binding in cexpr &#124;}</code>|<code>let binding in {&#124; cexpr &#124;}</code>|
|<code>{&#124; let! pattern = expr in cexpr &#124;}</code>|<code>builder.Bind(expr, (fun pattern -> {&#124; cexpr &#124;}))</code>|
|<code>{&#124; do! expr in cexpr &#124;}</code>|<code>builder.Bind(expr, (fun () -> {&#124; cexpr &#124;}))</code>|
|<code>{&#124; yield expr &#124;}</code>|`builder.Yield(expr)`|
|<code>{&#124; yield! expr &#124;}</code>|`builder.YieldFrom(expr)`|
|<code>{&#124; return expr &#124;}<code>|`builder.Return(expr)`|
|<code>{&#124; return! expr &#124;}</code>|`builder.ReturnFrom(expr)`|
|<code>{&#124; use pattern = expr in cexpr &#124;}</code>|<code>builder.Using(expr, (fun pattern -> {&#124; cexpr &#124;}))</code>|
|<code>{&#124; use! value = expr in cexpr &#124;}</code>|<code>builder.Bind(expr, (fun value -> builder.Using(value, (fun value -> {&#124; cexpr &#124;}))))</code>|
|<code>{&#124; if expr then cexpr0 &#124;}</code>|<code>if expr then {&#124; cexpr0 &#124;} else binder.Zero()</code>|
|<code>{&#124; if expr then cexpr0 else cexpr1 &#124;}</code>|<code>if expr then {&#124; cexpr0 &#124;} else {&#124; cexpr1 &#124;}</code>|
|<code>{&#124; match expr with &#124; pattern_i -> cexpr_i &#124;}</code>|<code>match expr with &#124; pattern_i -> {&#124; cexpr_i &#124;}</code>|
|<code>{&#124; for pattern in expr do cexpr &#124;}</code>|<code>builder.For(enumeration, (fun pattern -> {&#124; cexpr &#124;}))</code>|
|<code>{&#124; for identifier = expr1 to expr2 do cexpr &#124;}<code>|<code>builder.For(enumeration, (fun identifier -> {&#124; cexpr &#124;}))</code>|
|<code>{&#124; while expr do cexpr &#124;}</code>|<code>builder.While(fun () -> expr), builder.Delay({&#124;cexpr &#124;})</code>|
|<code>{&#124; try cexpr with &#124; pattern_i -> expr_i &#124;}</code>|<code>builder.TryWith(builder.Delay({&#124; cexpr &#124;}), (fun value -> match value with &#124; pattern_i -> expr_i &#124; exn -> reraise exn)))</code>|
|<code>{&#124; try cexpr finally expr &#124;}</code>|<code>builder.TryFinally(builder.Delay( {&#124; cexpr &#124;}), (fun () -> expr))</code>|
|<code>{&#124; cexpr1; cexpr2 &#124;}</code>|<code>builder.Combine({&#124;cexpr1 &#124;}, {&#124; cexpr2 &#124;})</code>|
|<code>{&#124; other-expr; cexpr &#124;}</code>|<code>expr; {&#124; cexpr &#124;}</code>|
|<code>{&#124; other-expr &#124;}</code>|`expr; builder.Zero()`|
<span data-ttu-id="89943-155">Dans le tableau précédent, `other-expr` décrit une expression qui ne figure pas dans le cas contraire dans la table.</span><span class="sxs-lookup"><span data-stu-id="89943-155">In the previous table, `other-expr` describes an expression that is not otherwise listed in the table.</span></span> <span data-ttu-id="89943-156">Une classe de générateur n’a pas besoin d’implémenter toutes les méthodes et de prendre en charge toutes les traductions répertoriées dans le tableau précédent.</span><span class="sxs-lookup"><span data-stu-id="89943-156">A builder class does not need to implement all of the methods and support all of the translations listed in the previous table.</span></span> <span data-ttu-id="89943-157">Ces constructions qui ne sont pas implémentées ne sont pas disponibles dans les expressions de calcul de ce type.</span><span class="sxs-lookup"><span data-stu-id="89943-157">Those constructs that are not implemented are not available in computation expressions of that type.</span></span> <span data-ttu-id="89943-158">Par exemple, si vous ne souhaitez pas prendre en charge la `use` mot clé dans les expressions de calcul, vous pouvez omettre la définition de `Use` dans votre classe de générateur.</span><span class="sxs-lookup"><span data-stu-id="89943-158">For example, if you do not want to support the `use` keyword in your computation expressions, you can omit the definition of `Use` in your builder class.</span></span>

<span data-ttu-id="89943-159">L’exemple de code suivant montre une expression de calcul qui encapsule un calcul, telle qu’une série d’étapes qui peut être évaluée une seule étape à la fois.</span><span class="sxs-lookup"><span data-stu-id="89943-159">The following code example shows a computation expression that encapsulates a computation as a series of steps that can be evaluated one step at a time.</span></span> <span data-ttu-id="89943-160">Un type d’union, de différencier `OkOrException`, encode l’état d’erreur de l’expression, telle qu’évaluée jusqu'à présent.</span><span class="sxs-lookup"><span data-stu-id="89943-160">A discriminated union type, `OkOrException`, encodes the error state of the expression as evaluated so far.</span></span> <span data-ttu-id="89943-161">Ce code illustre plusieurs modèles communs que vous pouvez utiliser dans vos expressions de calcul, telles que des implémentations de certaines méthodes de générateur réutilisable.</span><span class="sxs-lookup"><span data-stu-id="89943-161">This code demonstrates several typical patterns that you can use in your computation expressions, such as boilerplate implementations of some of the builder methods.</span></span>

```fsharp
// Computations that can be run step by step
type Eventually<'T> =
    | Done of 'T
    | NotYetDone of (unit -> Eventually<'T>)

module Eventually =
    // The bind for the computations. Append 'func' to the
    // computation.
    let rec bind func expr =
        match expr with
        | Done value -> NotYetDone (fun () -> func value)
        | NotYetDone work -> NotYetDone (fun () -> bind func (work()))

    // Return the final value wrapped in the Eventually type.
    let result value = Done value

    type OkOrException<'T> =
        | Ok of 'T
        | Exception of System.Exception

    // The catch for the computations. Stitch try/with throughout
    // the computation, and return the overall result as an OkOrException.
    let rec catch expr =
        match expr with
        | Done value -> result (Ok value)
        | NotYetDone work ->
            NotYetDone (fun () ->
                let res = try Ok(work()) with | exn -> Exception exn
                match res with
                | Ok cont -> catch cont // note, a tailcall
                | Exception exn -> result (Exception exn))

    // The delay operator.
    let delay func = NotYetDone (fun () -> func())

    // The stepping action for the computations.
    let step expr =
        match expr with
        | Done _ -> expr
        | NotYetDone func -> func ()

    // The rest of the operations are boilerplate.
    // The tryFinally operator.
    // This is boilerplate in terms of "result", "catch", and "bind".
    let tryFinally expr compensation =
        catch (expr)
        |> bind (fun res -> 
            compensation();
            match res with
            | Ok value -> result value
            | Exception exn -> raise exn)

    // The tryWith operator.
    // This is boilerplate in terms of "result", "catch", and "bind".
    let tryWith exn handler =
        catch exn
        |> bind (function Ok value -> result value | Exception exn -> handler exn)

    // The whileLoop operator.
    // This is boilerplate in terms of "result" and "bind".
    let rec whileLoop pred body =
        if pred() then body |> bind (fun _ -> whileLoop pred body)
        else result ()

    // The sequential composition operator.
    // This is boilerplate in terms of "result" and "bind".
    let combine expr1 expr2 =
        expr1 |> bind (fun () -> expr2)

    // The using operator.
    let using (resource: #System.IDisposable) func =
        tryFinally (func resource) (fun () -> resource.Dispose())

    // The forLoop operator.
    // This is boilerplate in terms of "catch", "result", and "bind".
    let forLoop (collection:seq<_>) func =
        let ie = collection.GetEnumerator()
        tryFinally 
            (whileLoop 
                (fun () -> ie.MoveNext()) 
                (delay (fun () -> let value = ie.Current in func value)))
            (fun () -> ie.Dispose())

// The builder class.
type EventuallyBuilder() =
    member x.Bind(comp, func) = Eventually.bind func comp
    member x.Return(value) = Eventually.result value
    member x.ReturnFrom(value) = value
    member x.Combine(expr1, expr2) = Eventually.combine expr1 expr2
    member x.Delay(func) = Eventually.delay func
    member x.Zero() = Eventually.result ()
    member x.TryWith(expr, handler) = Eventually.tryWith expr handler
    member x.TryFinally(expr, compensation) = Eventually.tryFinally expr compensation
    member x.For(coll:seq<_>, func) = Eventually.forLoop coll func
    member x.Using(resource, expr) = Eventually.using resource expr

let eventually = new EventuallyBuilder()

let comp = eventually {
    for x in 1..2 do
        printfn " x = %d" x
    return 3 + 4 }

// Try the remaining lines in F# interactive to see how this 
// computation expression works in practice.
let step x = Eventually.step x

// returns "NotYetDone <closure>"
comp |> step

// prints "x = 1"
// returns "NotYetDone <closure>"
comp |> step |> step

// prints "x = 1"
// prints "x = 2"
// returns "NotYetDone <closure>"
comp |> step |> step |> step |> step |> step |> step

// prints "x = 1"
// prints "x = 2"
// returns "Done 7"
comp |> step |> step |> step |> step |> step |> step |> step |> step
```

<span data-ttu-id="89943-162">Une expression de calcul possède un type sous-jacent, ce qui renvoie de l’expression.</span><span class="sxs-lookup"><span data-stu-id="89943-162">A computation expression has an underlying type, which the expression returns.</span></span> <span data-ttu-id="89943-163">Le type sous-jacent peut représenter un résultat calculées ou un calcul retardé qui peut être effectué, ou elle peut fournir un moyen pour une itération au sein d’un type de collection.</span><span class="sxs-lookup"><span data-stu-id="89943-163">The underlying type may represent a computed result or a delayed computation that can be performed, or it may provide a way to iterate through some type of collection.</span></span> <span data-ttu-id="89943-164">Dans l’exemple précédent, le type sous-jacent a été **finalement**.</span><span class="sxs-lookup"><span data-stu-id="89943-164">In the previous example, the underlying type was **Eventually**.</span></span> <span data-ttu-id="89943-165">Pour une expression de séquence, le type sous-jacent est <xref:System.Collections.Generic.IEnumerable%601?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="89943-165">For a sequence expression, the underlying type is <xref:System.Collections.Generic.IEnumerable%601?displayProperty=nameWithType>.</span></span> <span data-ttu-id="89943-166">Pour une expression de requête, le type sous-jacent est <xref:System.Linq.IQueryable?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="89943-166">For a query expression, the underlying type is <xref:System.Linq.IQueryable?displayProperty=nameWithType>.</span></span> <span data-ttu-id="89943-167">Pour un flux de travail asynchrone, le type sous-jacent est [ `Async` ](https://msdn.microsoft.com/library/03eb4d12-a01a-4565-a077-5e83f17cf6f7).</span><span class="sxs-lookup"><span data-stu-id="89943-167">For an asychronous workflow, the underlying type is [`Async`](https://msdn.microsoft.com/library/03eb4d12-a01a-4565-a077-5e83f17cf6f7).</span></span> <span data-ttu-id="89943-168">Le `Async` objet représente le travail à effectuer pour calculer le résultat.</span><span class="sxs-lookup"><span data-stu-id="89943-168">The `Async` object represents the work to be performed to compute the result.</span></span> <span data-ttu-id="89943-169">Par exemple, vous appelez [ `Async.RunSynchronously` ](https://msdn.microsoft.com/library/0a6663a9-50f2-4d38-8bf3-cefd1a51fd6b) pour exécuter un calcul et de retourner le résultat.</span><span class="sxs-lookup"><span data-stu-id="89943-169">For example, you call [`Async.RunSynchronously`](https://msdn.microsoft.com/library/0a6663a9-50f2-4d38-8bf3-cefd1a51fd6b) to execute a computation and return the result.</span></span>

## <a name="custom-operations"></a><span data-ttu-id="89943-170">Opérations personnalisées</span><span class="sxs-lookup"><span data-stu-id="89943-170">Custom Operations</span></span>
<span data-ttu-id="89943-171">Vous pouvez définir une opération personnalisée sur une expression de calcul et utiliser une opération personnalisée en tant qu’opérateur dans une expression de calcul.</span><span class="sxs-lookup"><span data-stu-id="89943-171">You can define a custom operation on a computation expression and use a custom operation as an operator in a computation expression.</span></span> <span data-ttu-id="89943-172">Par exemple, vous pouvez inclure un opérateur de requête dans une expression de requête.</span><span class="sxs-lookup"><span data-stu-id="89943-172">For example, you can include a query operator in a query expression.</span></span> <span data-ttu-id="89943-173">Lorsque vous définissez une opération personnalisée, vous devez définir le taux de rendement et les méthodes dans l’expression de calcul.</span><span class="sxs-lookup"><span data-stu-id="89943-173">When you define a custom operation, you must define the Yield and For methods in the computation expression.</span></span> <span data-ttu-id="89943-174">Pour définir une opération personnalisée, placée dans une classe de générateur pour l’expression de calcul, puis appliquez le [ `CustomOperationAttribute` ](https://msdn.microsoft.com/library/199f3927-79df-484b-ba66-85f58cc49b19).</span><span class="sxs-lookup"><span data-stu-id="89943-174">To define a custom operation, put it in a builder class for the computation expression, and then apply the [`CustomOperationAttribute`](https://msdn.microsoft.com/library/199f3927-79df-484b-ba66-85f58cc49b19).</span></span> <span data-ttu-id="89943-175">Cet attribut prend une chaîne en tant qu’argument, qui est le nom à utiliser dans une opération personnalisée.</span><span class="sxs-lookup"><span data-stu-id="89943-175">This attribute takes a string as an argument, which is the name to be used in a custom operation.</span></span> <span data-ttu-id="89943-176">Ce nom est fourni dans la portée au début de l’accolade ouvrante de l’expression de calcul.</span><span class="sxs-lookup"><span data-stu-id="89943-176">This name comes into scope at the start of the opening curly brace of the computation expression.</span></span> <span data-ttu-id="89943-177">Par conséquent, vous ne devez pas utiliser des identificateurs qui ont le même nom qu’une opération personnalisée dans ce bloc.</span><span class="sxs-lookup"><span data-stu-id="89943-177">Therefore, you shouldn’t use identifiers that have the same name as a custom operation in this block.</span></span> <span data-ttu-id="89943-178">Par exemple, évitez l’utilisation des identificateurs comme `all` ou `last` dans les expressions de requête.</span><span class="sxs-lookup"><span data-stu-id="89943-178">For example, avoid the use of identifiers such as `all` or `last` in query expressions.</span></span>

## <a name="see-also"></a><span data-ttu-id="89943-179">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="89943-179">See Also</span></span>
[<span data-ttu-id="89943-180">Informations de référence du langage F#</span><span class="sxs-lookup"><span data-stu-id="89943-180">F# Language Reference</span></span>](index.md)

[<span data-ttu-id="89943-181">Flux de travail asynchrones</span><span class="sxs-lookup"><span data-stu-id="89943-181">Asynchronous Workflows</span></span>](asynchronous-workflows.md)

[<span data-ttu-id="89943-182">Séquences</span><span class="sxs-lookup"><span data-stu-id="89943-182">Sequences</span></span>](https://msdn.microsoft.com/library/6b773b6b-9c9a-4af8-bd9e-d96585c166db)

[<span data-ttu-id="89943-183">Expressions de requête</span><span class="sxs-lookup"><span data-stu-id="89943-183">Query Expressions</span></span>](query-expressions.md)