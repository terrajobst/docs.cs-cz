---
title: PasswordBox – styly a šablony
ms.date: 03/30/2017
helpviewer_keywords:
- styles [WPF], PasswordBox
- templates [WPF], PasswordBox
- ControlTemplate [WPF], PasswordBox
- states [WPF], PasswordBox
- PasswordBox [WPF], styles and templates
- parts [WPF], PasswordBox
ms.assetid: deb52107-959f-4a60-b303-d21a0a933060
ms.openlocfilehash: 7783330dd56ec5b2759e783a6935761eb3587978
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2019
ms.locfileid: "57507298"
---
# <a name="passwordbox-styles-and-templates"></a><span data-ttu-id="2b8fc-102">PasswordBox – styly a šablony</span><span class="sxs-lookup"><span data-stu-id="2b8fc-102">PasswordBox Styles and Templates</span></span>

<span data-ttu-id="2b8fc-103">Toto téma popisuje styly a šablony pro <xref:System.Windows.Controls.PasswordBox> ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-103">This topic describes the styles and templates for the <xref:System.Windows.Controls.PasswordBox> control.</span></span> <span data-ttu-id="2b8fc-104">Můžete upravit výchozí <xref:System.Windows.Controls.ControlTemplate> poskytnout jedinečný vzhled ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-104">You can modify the default <xref:System.Windows.Controls.ControlTemplate> to give the control a unique appearance.</span></span> <span data-ttu-id="2b8fc-105">Další informace najdete v tématu [přizpůsobení vzhledu stávajícího ovládacího prvku vytvořením ControlTemplate](customizing-the-appearance-of-an-existing-control.md).</span><span class="sxs-lookup"><span data-stu-id="2b8fc-105">For more information, see [Customizing the Appearance of an Existing Control by Creating a ControlTemplate](customizing-the-appearance-of-an-existing-control.md).</span></span>

## <a name="passwordbox-parts"></a><span data-ttu-id="2b8fc-106">Části pole pro zadání hesla</span><span class="sxs-lookup"><span data-stu-id="2b8fc-106">PasswordBox Parts</span></span>

<span data-ttu-id="2b8fc-107">V následující tabulce jsou uvedeny pojmenované části pro <xref:System.Windows.Controls.PasswordBox> ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-107">The following table lists the named parts for the <xref:System.Windows.Controls.PasswordBox> control.</span></span>

|<span data-ttu-id="2b8fc-108">Část</span><span class="sxs-lookup"><span data-stu-id="2b8fc-108">Part</span></span>|<span data-ttu-id="2b8fc-109">Typ</span><span class="sxs-lookup"><span data-stu-id="2b8fc-109">Type</span></span>|<span data-ttu-id="2b8fc-110">Popis</span><span class="sxs-lookup"><span data-stu-id="2b8fc-110">Description</span></span>|
|-|-|-|
|<span data-ttu-id="2b8fc-111">PART_ContentHost</span><span class="sxs-lookup"><span data-stu-id="2b8fc-111">PART_ContentHost</span></span>|<xref:System.Windows.FrameworkElement>|<span data-ttu-id="2b8fc-112">Vizuální prvek, který může obsahovat <xref:System.Windows.FrameworkElement>.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-112">A visual element that can contain a <xref:System.Windows.FrameworkElement>.</span></span> <span data-ttu-id="2b8fc-113">Text <xref:System.Windows.Controls.PasswordBox> se zobrazí v tomto elementu.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-113">The text of the <xref:System.Windows.Controls.PasswordBox> is displayed in this element.</span></span>|

## <a name="passwordbox-states"></a><span data-ttu-id="2b8fc-114">Stavy pole pro zadání hesla</span><span class="sxs-lookup"><span data-stu-id="2b8fc-114">PasswordBox States</span></span>

<span data-ttu-id="2b8fc-115">V následující tabulce jsou uvedeny vizuálních stavů pro <xref:System.Windows.Controls.PasswordBox> ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-115">The following table lists the visual states for the <xref:System.Windows.Controls.PasswordBox> control.</span></span>

|<span data-ttu-id="2b8fc-116">Název vizuálního stavu</span><span class="sxs-lookup"><span data-stu-id="2b8fc-116">VisualState Name</span></span>|<span data-ttu-id="2b8fc-117">Název VisualStateGroup</span><span class="sxs-lookup"><span data-stu-id="2b8fc-117">VisualStateGroup Name</span></span>|<span data-ttu-id="2b8fc-118">Popis</span><span class="sxs-lookup"><span data-stu-id="2b8fc-118">Description</span></span>|
|-|-|-|
|<span data-ttu-id="2b8fc-119">Normální</span><span class="sxs-lookup"><span data-stu-id="2b8fc-119">Normal</span></span>|<span data-ttu-id="2b8fc-120">CommonStates</span><span class="sxs-lookup"><span data-stu-id="2b8fc-120">CommonStates</span></span>|<span data-ttu-id="2b8fc-121">Ve výchozím stavu.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-121">The default state.</span></span>|
|<span data-ttu-id="2b8fc-122">Myš nad</span><span class="sxs-lookup"><span data-stu-id="2b8fc-122">MouseOver</span></span>|<span data-ttu-id="2b8fc-123">CommonStates</span><span class="sxs-lookup"><span data-stu-id="2b8fc-123">CommonStates</span></span>|<span data-ttu-id="2b8fc-124">Je ukazatel myši umístěn nad ovládací prvek.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-124">The mouse pointer is positioned over the control.</span></span>|
|<span data-ttu-id="2b8fc-125">Zakázáno</span><span class="sxs-lookup"><span data-stu-id="2b8fc-125">Disabled</span></span>|<span data-ttu-id="2b8fc-126">CommonStates</span><span class="sxs-lookup"><span data-stu-id="2b8fc-126">CommonStates</span></span>|<span data-ttu-id="2b8fc-127">Ovládací prvek je zakázaný.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-127">The control is disabled.</span></span>|
|<span data-ttu-id="2b8fc-128">Fokus</span><span class="sxs-lookup"><span data-stu-id="2b8fc-128">Focused</span></span>|<span data-ttu-id="2b8fc-129">FocusStates</span><span class="sxs-lookup"><span data-stu-id="2b8fc-129">FocusStates</span></span>|<span data-ttu-id="2b8fc-130">Ovládací prvek má fokus.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-130">The control has focus.</span></span>|
|<span data-ttu-id="2b8fc-131">Bez fokusu</span><span class="sxs-lookup"><span data-stu-id="2b8fc-131">Unfocused</span></span>|<span data-ttu-id="2b8fc-132">FocusStates</span><span class="sxs-lookup"><span data-stu-id="2b8fc-132">FocusStates</span></span>|<span data-ttu-id="2b8fc-133">Ovládací prvek nemá fokus.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-133">The control does not have focus.</span></span>|
|<span data-ttu-id="2b8fc-134">Platné</span><span class="sxs-lookup"><span data-stu-id="2b8fc-134">Valid</span></span>|<span data-ttu-id="2b8fc-135">ValidationStates</span><span class="sxs-lookup"><span data-stu-id="2b8fc-135">ValidationStates</span></span>|<span data-ttu-id="2b8fc-136">Ovládací prvek používá <xref:System.Windows.Controls.Validation> třídy a <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> je připojená vlastnost `false`.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-136">The control uses the <xref:System.Windows.Controls.Validation> class and the <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> attached property is `false`.</span></span>|
|<span data-ttu-id="2b8fc-137">InvalidFocused</span><span class="sxs-lookup"><span data-stu-id="2b8fc-137">InvalidFocused</span></span>|<span data-ttu-id="2b8fc-138">ValidationStates</span><span class="sxs-lookup"><span data-stu-id="2b8fc-138">ValidationStates</span></span>|<span data-ttu-id="2b8fc-139"><xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> Je připojená vlastnost `true` má ovládací prvek má fokus.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-139">The <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> attached property is `true` has the control has focus.</span></span>|
|<span data-ttu-id="2b8fc-140">InvalidUnfocused</span><span class="sxs-lookup"><span data-stu-id="2b8fc-140">InvalidUnfocused</span></span>|<span data-ttu-id="2b8fc-141">ValidationStates</span><span class="sxs-lookup"><span data-stu-id="2b8fc-141">ValidationStates</span></span>|<span data-ttu-id="2b8fc-142"><xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> Je připojená vlastnost `true` má ovládací prvek nemá fokus.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-142">The <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> attached property is `true` has the control does not have focus.</span></span>|

## <a name="passwordbox-controltemplate-example"></a><span data-ttu-id="2b8fc-143">Příklad šablony ControlTemplate pole pro zadání hesla</span><span class="sxs-lookup"><span data-stu-id="2b8fc-143">PasswordBox ControlTemplate Example</span></span>

<span data-ttu-id="2b8fc-144">Následující příklad ukazuje, jak definovat <xref:System.Windows.Controls.ControlTemplate> pro <xref:System.Windows.Controls.PasswordBox> ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-144">The following example shows how to define a <xref:System.Windows.Controls.ControlTemplate> for the <xref:System.Windows.Controls.PasswordBox> control.</span></span>

[!code-xaml[ControlTemplateExamples#PasswordBox](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/textbox.xaml#passwordbox)]

<span data-ttu-id="2b8fc-145">V předchozím příkladu používá jeden nebo více z následujících prostředků.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-145">The preceding example uses one or more of the following resources.</span></span>

[!code-xaml[ControlTemplateExamples#Resources](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/shared.xaml#resources)]

<span data-ttu-id="2b8fc-146">Úplnou ukázku najdete v tématu [stylu s ukázkou ControlTemplates](https://github.com/Microsoft/WPF-Samples/tree/master/Styles%20&%20Templates/IntroToStylingAndTemplating).</span><span class="sxs-lookup"><span data-stu-id="2b8fc-146">For the complete sample, see [Styling with ControlTemplates Sample](https://github.com/Microsoft/WPF-Samples/tree/master/Styles%20&%20Templates/IntroToStylingAndTemplating).</span></span>

## <a name="see-also"></a><span data-ttu-id="2b8fc-147">Viz také:</span><span class="sxs-lookup"><span data-stu-id="2b8fc-147">See also</span></span>

- <xref:System.Windows.FrameworkElement.Style%2A>
- <xref:System.Windows.Controls.ControlTemplate>
- [<span data-ttu-id="2b8fc-148">Styly a šablony ovládacích prvků</span><span class="sxs-lookup"><span data-stu-id="2b8fc-148">Control Styles and Templates</span></span>](control-styles-and-templates.md)
- [<span data-ttu-id="2b8fc-149">Přizpůsobení ovládacího prvku</span><span class="sxs-lookup"><span data-stu-id="2b8fc-149">Control Customization</span></span>](control-customization.md)
- [<span data-ttu-id="2b8fc-150">Styly a šablony</span><span class="sxs-lookup"><span data-stu-id="2b8fc-150">Styling and Templating</span></span>](styling-and-templating.md)
- [<span data-ttu-id="2b8fc-151">Přizpůsobení vzhledu stávajícího ovládacího prvku vytvořením šablony ControlTemplate</span><span class="sxs-lookup"><span data-stu-id="2b8fc-151">Customizing the Appearance of an Existing Control by Creating a ControlTemplate</span></span>](customizing-the-appearance-of-an-existing-control.md)