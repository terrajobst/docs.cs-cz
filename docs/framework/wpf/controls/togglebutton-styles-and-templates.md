---
title: ToggleButton – styly a šablony
ms.date: 03/30/2017
helpviewer_keywords:
- states [WPF], ToggleButton
- ToggleButton [WPF], styles and templates
- ControlTemplate [WPF], ToggleButton
- styles [WPF], ToggleButton
- templates [WPF], ToggleButton
- parts [WPF], ToggleButton
ms.assetid: 54f23f30-4bcb-4f09-8ce4-376a13a255a1
ms.openlocfilehash: 46fd7d07c3904ee752ae3f467f65af4b0c031c84
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2019
ms.locfileid: "57507292"
---
# <a name="togglebutton-styles-and-templates"></a><span data-ttu-id="cf24a-102">ToggleButton – styly a šablony</span><span class="sxs-lookup"><span data-stu-id="cf24a-102">ToggleButton Styles and Templates</span></span>

<span data-ttu-id="cf24a-103">Toto téma popisuje styly a šablony pro <xref:System.Windows.Controls.Primitives.ToggleButton> ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="cf24a-103">This topic describes the styles and templates for the <xref:System.Windows.Controls.Primitives.ToggleButton> control.</span></span> <span data-ttu-id="cf24a-104">Můžete upravit výchozí <xref:System.Windows.Controls.ControlTemplate> poskytnout jedinečný vzhled ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="cf24a-104">You can modify the default <xref:System.Windows.Controls.ControlTemplate> to give the control a unique appearance.</span></span> <span data-ttu-id="cf24a-105">Další informace najdete v tématu [přizpůsobení vzhledu stávajícího ovládacího prvku vytvořením ControlTemplate](customizing-the-appearance-of-an-existing-control.md).</span><span class="sxs-lookup"><span data-stu-id="cf24a-105">For more information, see [Customizing the Appearance of an Existing Control by Creating a ControlTemplate](customizing-the-appearance-of-an-existing-control.md).</span></span>

## <a name="togglebutton-parts"></a><span data-ttu-id="cf24a-106">Části ToggleButton</span><span class="sxs-lookup"><span data-stu-id="cf24a-106">ToggleButton Parts</span></span>

<span data-ttu-id="cf24a-107"><xref:System.Windows.Controls.Primitives.ToggleButton> Ovládací prvek nemá žádné pojmenované součásti.</span><span class="sxs-lookup"><span data-stu-id="cf24a-107">The <xref:System.Windows.Controls.Primitives.ToggleButton> control does not have any named parts.</span></span>

## <a name="togglebutton-states"></a><span data-ttu-id="cf24a-108">Stavy ToggleButton</span><span class="sxs-lookup"><span data-stu-id="cf24a-108">ToggleButton States</span></span>

<span data-ttu-id="cf24a-109">V následující tabulce jsou uvedeny vizuálních stavů pro <xref:System.Windows.Controls.Primitives.ToggleButton> ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="cf24a-109">The following table lists the visual states for the <xref:System.Windows.Controls.Primitives.ToggleButton> control.</span></span>

|<span data-ttu-id="cf24a-110">Název vizuálního stavu</span><span class="sxs-lookup"><span data-stu-id="cf24a-110">VisualState Name</span></span>|<span data-ttu-id="cf24a-111">Název VisualStateGroup</span><span class="sxs-lookup"><span data-stu-id="cf24a-111">VisualStateGroup Name</span></span>|<span data-ttu-id="cf24a-112">Popis</span><span class="sxs-lookup"><span data-stu-id="cf24a-112">Description</span></span>|
|-|-|-|
|<span data-ttu-id="cf24a-113">Normální</span><span class="sxs-lookup"><span data-stu-id="cf24a-113">Normal</span></span>|<span data-ttu-id="cf24a-114">CommonStates</span><span class="sxs-lookup"><span data-stu-id="cf24a-114">CommonStates</span></span>|<span data-ttu-id="cf24a-115">Ve výchozím stavu.</span><span class="sxs-lookup"><span data-stu-id="cf24a-115">The default state.</span></span>|
|<span data-ttu-id="cf24a-116">Myš nad</span><span class="sxs-lookup"><span data-stu-id="cf24a-116">MouseOver</span></span>|<span data-ttu-id="cf24a-117">CommonStates</span><span class="sxs-lookup"><span data-stu-id="cf24a-117">CommonStates</span></span>|<span data-ttu-id="cf24a-118">Je ukazatel myši umístěn nad ovládací prvek.</span><span class="sxs-lookup"><span data-stu-id="cf24a-118">The mouse pointer is positioned over the control.</span></span>|
|<span data-ttu-id="cf24a-119">Stisknutí</span><span class="sxs-lookup"><span data-stu-id="cf24a-119">Pressed</span></span>|<span data-ttu-id="cf24a-120">CommonStates</span><span class="sxs-lookup"><span data-stu-id="cf24a-120">CommonStates</span></span>|<span data-ttu-id="cf24a-121">Stisknutí ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="cf24a-121">The control is pressed.</span></span>|
|<span data-ttu-id="cf24a-122">Zakázáno</span><span class="sxs-lookup"><span data-stu-id="cf24a-122">Disabled</span></span>|<span data-ttu-id="cf24a-123">CommonStates</span><span class="sxs-lookup"><span data-stu-id="cf24a-123">CommonStates</span></span>|<span data-ttu-id="cf24a-124">Ovládací prvek je zakázaný.</span><span class="sxs-lookup"><span data-stu-id="cf24a-124">The control is disabled.</span></span>|
|<span data-ttu-id="cf24a-125">Fokus</span><span class="sxs-lookup"><span data-stu-id="cf24a-125">Focused</span></span>|<span data-ttu-id="cf24a-126">FocusStates</span><span class="sxs-lookup"><span data-stu-id="cf24a-126">FocusStates</span></span>|<span data-ttu-id="cf24a-127">Ovládací prvek má fokus.</span><span class="sxs-lookup"><span data-stu-id="cf24a-127">The control has focus.</span></span>|
|<span data-ttu-id="cf24a-128">Bez fokusu</span><span class="sxs-lookup"><span data-stu-id="cf24a-128">Unfocused</span></span>|<span data-ttu-id="cf24a-129">FocusStates</span><span class="sxs-lookup"><span data-stu-id="cf24a-129">FocusStates</span></span>|<span data-ttu-id="cf24a-130">Ovládací prvek nemá fokus.</span><span class="sxs-lookup"><span data-stu-id="cf24a-130">The control does not have focus.</span></span>|
|<span data-ttu-id="cf24a-131">Zaškrtnuto</span><span class="sxs-lookup"><span data-stu-id="cf24a-131">Checked</span></span>|<span data-ttu-id="cf24a-132">CheckStates</span><span class="sxs-lookup"><span data-stu-id="cf24a-132">CheckStates</span></span>|<span data-ttu-id="cf24a-133"><xref:System.Windows.Controls.Primitives.ToggleButton.IsChecked%2A> je `true`.</span><span class="sxs-lookup"><span data-stu-id="cf24a-133"><xref:System.Windows.Controls.Primitives.ToggleButton.IsChecked%2A> is `true`.</span></span>|
|<span data-ttu-id="cf24a-134">Není zaškrtnuto</span><span class="sxs-lookup"><span data-stu-id="cf24a-134">Unchecked</span></span>|<span data-ttu-id="cf24a-135">CheckStates</span><span class="sxs-lookup"><span data-stu-id="cf24a-135">CheckStates</span></span>|<span data-ttu-id="cf24a-136"><xref:System.Windows.Controls.Primitives.ToggleButton.IsChecked%2A> je `false`.</span><span class="sxs-lookup"><span data-stu-id="cf24a-136"><xref:System.Windows.Controls.Primitives.ToggleButton.IsChecked%2A> is `false`.</span></span>|
|<span data-ttu-id="cf24a-137">Neurčitá</span><span class="sxs-lookup"><span data-stu-id="cf24a-137">Indeterminate</span></span>|<span data-ttu-id="cf24a-138">CheckStates</span><span class="sxs-lookup"><span data-stu-id="cf24a-138">CheckStates</span></span>|<span data-ttu-id="cf24a-139"><xref:System.Windows.Controls.Primitives.ToggleButton.IsThreeState%2A> je `true`, a <xref:System.Windows.Controls.Primitives.ToggleButton.IsChecked%2A> je `null`.</span><span class="sxs-lookup"><span data-stu-id="cf24a-139"><xref:System.Windows.Controls.Primitives.ToggleButton.IsThreeState%2A> is `true`, and <xref:System.Windows.Controls.Primitives.ToggleButton.IsChecked%2A> is `null`.</span></span>|
|<span data-ttu-id="cf24a-140">Platné</span><span class="sxs-lookup"><span data-stu-id="cf24a-140">Valid</span></span>|<span data-ttu-id="cf24a-141">ValidationStates</span><span class="sxs-lookup"><span data-stu-id="cf24a-141">ValidationStates</span></span>|<span data-ttu-id="cf24a-142">Ovládací prvek používá <xref:System.Windows.Controls.Validation> třídy a <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> je připojená vlastnost `false`.</span><span class="sxs-lookup"><span data-stu-id="cf24a-142">The control uses the <xref:System.Windows.Controls.Validation> class and the <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> attached property is `false`.</span></span>|
|<span data-ttu-id="cf24a-143">InvalidFocused</span><span class="sxs-lookup"><span data-stu-id="cf24a-143">InvalidFocused</span></span>|<span data-ttu-id="cf24a-144">ValidationStates</span><span class="sxs-lookup"><span data-stu-id="cf24a-144">ValidationStates</span></span>|<span data-ttu-id="cf24a-145"><xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> Je připojená vlastnost `true` má ovládací prvek má fokus.</span><span class="sxs-lookup"><span data-stu-id="cf24a-145">The <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> attached property is `true` has the control has focus.</span></span>|
|<span data-ttu-id="cf24a-146">InvalidUnfocused</span><span class="sxs-lookup"><span data-stu-id="cf24a-146">InvalidUnfocused</span></span>|<span data-ttu-id="cf24a-147">ValidationStates</span><span class="sxs-lookup"><span data-stu-id="cf24a-147">ValidationStates</span></span>|<span data-ttu-id="cf24a-148"><xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> Je připojená vlastnost `true` má ovládací prvek nemá fokus.</span><span class="sxs-lookup"><span data-stu-id="cf24a-148">The <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> attached property is `true` has the control does not have focus.</span></span>|

> [!NOTE]
> <span data-ttu-id="cf24a-149">Pokud neurčitý vizuálního stavu v šabloně ovládacího prvku neexistuje, pak Nekontrolovaná vizuálního stavu se použije jako výchozí vizuálního stavu.</span><span class="sxs-lookup"><span data-stu-id="cf24a-149">If the Indeterminate visual state does not exist in your control template, then the Unchecked visual state will be used as default visual state.</span></span>

## <a name="togglebutton-controltemplate-example"></a><span data-ttu-id="cf24a-150">Příklad šablony ControlTemplate ToggleButton</span><span class="sxs-lookup"><span data-stu-id="cf24a-150">ToggleButton ControlTemplate Example</span></span>

<span data-ttu-id="cf24a-151">Následující příklad ukazuje, jak definovat <xref:System.Windows.Controls.ControlTemplate> pro <xref:System.Windows.Controls.Primitives.ToggleButton> ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="cf24a-151">The following example shows how to define a <xref:System.Windows.Controls.ControlTemplate> for the <xref:System.Windows.Controls.Primitives.ToggleButton> control.</span></span>

[!code-xaml[ControlTemplateExamples#ToggleButton](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/combobox.xaml#togglebutton)]

<span data-ttu-id="cf24a-152">V předchozím příkladu používá jeden nebo více z následujících prostředků.</span><span class="sxs-lookup"><span data-stu-id="cf24a-152">The preceding example uses one or more of the following resources.</span></span>

[!code-xaml[ControlTemplateExamples#Resources](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/shared.xaml#resources)]

<span data-ttu-id="cf24a-153">Úplnou ukázku najdete v tématu [stylu s ukázkou ControlTemplates](https://github.com/Microsoft/WPF-Samples/tree/master/Styles%20&%20Templates/IntroToStylingAndTemplating).</span><span class="sxs-lookup"><span data-stu-id="cf24a-153">For the complete sample, see [Styling with ControlTemplates Sample](https://github.com/Microsoft/WPF-Samples/tree/master/Styles%20&%20Templates/IntroToStylingAndTemplating).</span></span>

## <a name="see-also"></a><span data-ttu-id="cf24a-154">Viz také:</span><span class="sxs-lookup"><span data-stu-id="cf24a-154">See also</span></span>

- <xref:System.Windows.FrameworkElement.Style%2A>
- <xref:System.Windows.Controls.ControlTemplate>
- [<span data-ttu-id="cf24a-155">Styly a šablony ovládacích prvků</span><span class="sxs-lookup"><span data-stu-id="cf24a-155">Control Styles and Templates</span></span>](control-styles-and-templates.md)
- [<span data-ttu-id="cf24a-156">Přizpůsobení ovládacího prvku</span><span class="sxs-lookup"><span data-stu-id="cf24a-156">Control Customization</span></span>](control-customization.md)
- [<span data-ttu-id="cf24a-157">Styly a šablony</span><span class="sxs-lookup"><span data-stu-id="cf24a-157">Styling and Templating</span></span>](styling-and-templating.md)
- [<span data-ttu-id="cf24a-158">Přizpůsobení vzhledu stávajícího ovládacího prvku vytvořením šablony ControlTemplate</span><span class="sxs-lookup"><span data-stu-id="cf24a-158">Customizing the Appearance of an Existing Control by Creating a ControlTemplate</span></span>](customizing-the-appearance-of-an-existing-control.md)