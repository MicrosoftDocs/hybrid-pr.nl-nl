---
title: Het DevOps-patroon in Azure Stack hub
description: Meer informatie over het DevOps-patroon, zodat u consistentie kunt garanderen tussen implementaties in Azure en Azure Stack hub.
author: BryanLa
ms.topic: article
ms.date: 11/05/2019
ms.author: bryanla
ms.reviewer: anajod
ms.lastreviewed: 11/05/2019
ms.openlocfilehash: 306cc9604a8e919724f9f76b7e5122d534d2d1ae
ms.sourcegitcommit: bb3e40b210f86173568a47ba18c3cc50d4a40607
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/17/2020
ms.locfileid: "84910421"
---
# <a name="devops-pattern"></a><span data-ttu-id="1a17d-103">DevOps patroon</span><span class="sxs-lookup"><span data-stu-id="1a17d-103">DevOps pattern</span></span>

<span data-ttu-id="1a17d-104">Code vanaf één locatie en implementeren in meerdere doelen in ontwikkel-, test-en productie omgevingen die zich in uw lokale Data Center, persoonlijke Clouds of open bare cloud bevinden.</span><span class="sxs-lookup"><span data-stu-id="1a17d-104">Code from a single location and deploy to multiple targets in development, test, and production environments that may be in your local datacenter, private clouds, or the public cloud.</span></span>

## <a name="context-and-problem"></a><span data-ttu-id="1a17d-105">Context en probleem</span><span class="sxs-lookup"><span data-stu-id="1a17d-105">Context and problem</span></span>

<span data-ttu-id="1a17d-106">Continuïteit van de toepassings implementatie, beveiliging en betrouw baarheid zijn essentieel voor organisaties en essentieel voor ontwikkel teams.</span><span class="sxs-lookup"><span data-stu-id="1a17d-106">Application deployment continuity, security, and reliability are essential to organizations and critical to development teams.</span></span>

<span data-ttu-id="1a17d-107">Apps vereisen vaak herstructured code om in elke doel omgeving te worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1a17d-107">Apps often require refactored code to run in each target environment.</span></span> <span data-ttu-id="1a17d-108">Dit betekent dat een app niet volledig draagbaar is.</span><span class="sxs-lookup"><span data-stu-id="1a17d-108">This means that an app isn't completely portable.</span></span> <span data-ttu-id="1a17d-109">Het moet worden bijgewerkt, getest en gevalideerd terwijl het door elke omgeving heen wordt verplaatst.</span><span class="sxs-lookup"><span data-stu-id="1a17d-109">It must be updated, tested, and validated as it moves through each environment.</span></span> <span data-ttu-id="1a17d-110">Code die is geschreven in een ontwikkel omgeving moet vervolgens worden herschreven om te werken in een test omgeving en opnieuw te worden geschreven wanneer het uiteindelijk in een productie omgeving gaat.</span><span class="sxs-lookup"><span data-stu-id="1a17d-110">For example, code written in a development environment must then be rewritten to work in a test environment and rewritten when it finally lands in a production environment.</span></span> <span data-ttu-id="1a17d-111">Daarnaast is deze code specifiek gebonden aan de host.</span><span class="sxs-lookup"><span data-stu-id="1a17d-111">Furthermore, this code is specifically tied to the host.</span></span> <span data-ttu-id="1a17d-112">Dit verhoogt de kosten en complexiteit van het onderhouden van uw app.</span><span class="sxs-lookup"><span data-stu-id="1a17d-112">This increases the cost and complexity of maintaining your app.</span></span> <span data-ttu-id="1a17d-113">Elke versie van de app is gekoppeld aan elke omgeving.</span><span class="sxs-lookup"><span data-stu-id="1a17d-113">Each version of the app is tied to each environment.</span></span> <span data-ttu-id="1a17d-114">Dankzij de verbeterde complexiteit en duplicatie wordt het risico van beveiliging en code kwaliteit verhoogd.</span><span class="sxs-lookup"><span data-stu-id="1a17d-114">The increased complexity and duplication increase the risk of security and code quality.</span></span> <span data-ttu-id="1a17d-115">Daarnaast kan de code niet direct opnieuw worden geïmplementeerd wanneer u herstel hosts herstelt of extra hosts implementeert om toename in de vraag te verwerken.</span><span class="sxs-lookup"><span data-stu-id="1a17d-115">In addition, the code can't be readily redeployed when you remove restore failed hosts or deploy additional hosts to handle increases in demand.</span></span>

## <a name="solution"></a><span data-ttu-id="1a17d-116">Oplossing</span><span class="sxs-lookup"><span data-stu-id="1a17d-116">Solution</span></span>

<span data-ttu-id="1a17d-117">Met het DevOps-patroon kunt u een app bouwen, testen en implementeren die wordt uitgevoerd op meerdere clouds.</span><span class="sxs-lookup"><span data-stu-id="1a17d-117">The DevOps Pattern enables you to build, test, and deploy an app that runs on multiple clouds.</span></span> <span data-ttu-id="1a17d-118">Dit patroon is de praktijk eenheid voor continue integratie en continue levering.</span><span class="sxs-lookup"><span data-stu-id="1a17d-118">This pattern unites the practice of continuous integration and continuous delivery.</span></span> <span data-ttu-id="1a17d-119">Met doorlopende integratie wordt code gebouwd en getest wanneer een teamlid een wijziging doorvoert in versie beheer.</span><span class="sxs-lookup"><span data-stu-id="1a17d-119">With continuous integration, code is built and tested every time a team member commits a change to version control.</span></span> <span data-ttu-id="1a17d-120">Continue levering automatiseert elke stap van een build naar een productie omgeving.</span><span class="sxs-lookup"><span data-stu-id="1a17d-120">Continuous delivery automates each step from a build to a production environment.</span></span> <span data-ttu-id="1a17d-121">Samen maken deze processen een release proces dat ondersteuning biedt voor implementatie in diverse omgevingen.</span><span class="sxs-lookup"><span data-stu-id="1a17d-121">Together, these processes create a release process that supports deployment across diverse environments.</span></span> <span data-ttu-id="1a17d-122">Met dit patroon kunt u uw code ontwerpen en vervolgens dezelfde code implementeren in een lokale omgeving, verschillende privécloud en open bare Clouds.</span><span class="sxs-lookup"><span data-stu-id="1a17d-122">With this pattern, you can draft your code and then deploy the same code to a premise environment, different private clouds, and the public clouds.</span></span> <span data-ttu-id="1a17d-123">Verschillen in de omgeving vereisen een wijziging in een configuratie bestand in plaats van wijzigingen in de code.</span><span class="sxs-lookup"><span data-stu-id="1a17d-123">Differences in environment require a change to a configuration file rather than changes to the code.</span></span>

![DevOps patroon](media/pattern-cicd-pipeline/hybrid-ci-cd.png)

<span data-ttu-id="1a17d-125">Met een consistente set ontwikkel tools voor on-premises, privécloud en open bare Cloud omgevingen kunt u een praktijk van continue integratie en continue levering implementeren.</span><span class="sxs-lookup"><span data-stu-id="1a17d-125">With a consistent set of development tools across on-premises, private cloud, and public cloud environments, you can implement a practice of continuous integration and continuous delivery.</span></span> <span data-ttu-id="1a17d-126">Apps en services die zijn geïmplementeerd met behulp van het DevOps-patroon zijn uitwisselbaar en kunnen op elk van deze locaties worden uitgevoerd, waarbij gebruik wordt gemaakt van on-premises en open bare Cloud functies en-mogelijkheden.</span><span class="sxs-lookup"><span data-stu-id="1a17d-126">Apps and services deployed using the DevOps Pattern are interchangeable and can run in any of these locations, taking advantage of on-premises and public cloud features and capabilities.</span></span>

<span data-ttu-id="1a17d-127">Met een DevOps-release pijplijn kunt u het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="1a17d-127">Using a DevOps release pipeline helps you:</span></span>

- <span data-ttu-id="1a17d-128">Start een nieuwe build op basis van code doorvoeren aan één opslag plaats.</span><span class="sxs-lookup"><span data-stu-id="1a17d-128">Initiate a new build based on code commits to a single repository.</span></span>
- <span data-ttu-id="1a17d-129">Implementeer automatisch uw zojuist opgebouwde code naar de open bare Cloud voor acceptatie tests door gebruikers.</span><span class="sxs-lookup"><span data-stu-id="1a17d-129">Automatically deploy your newly built code to the public cloud for user acceptance testing.</span></span>
- <span data-ttu-id="1a17d-130">Automatisch implementeren in een privécloud nadat uw code is getest.</span><span class="sxs-lookup"><span data-stu-id="1a17d-130">Automatically deploy to a private cloud once your code has passed testing.</span></span>

## <a name="issues-and-considerations"></a><span data-ttu-id="1a17d-131">Problemen en overwegingen</span><span class="sxs-lookup"><span data-stu-id="1a17d-131">Issues and considerations</span></span>

<span data-ttu-id="1a17d-132">Het DevOps-patroon is bedoeld om consistentie tussen implementaties te garanderen, ongeacht de doel omgeving.</span><span class="sxs-lookup"><span data-stu-id="1a17d-132">The DevOps Pattern is intended to ensure consistency across deployments regardless of the target environment.</span></span> <span data-ttu-id="1a17d-133">De mogelijkheden verschillen echter in de Cloud-en on-premises omgevingen.</span><span class="sxs-lookup"><span data-stu-id="1a17d-133">However, capabilities vary across cloud and on-premises environments.</span></span> <span data-ttu-id="1a17d-134">Houd rekening met de volgende punten:</span><span class="sxs-lookup"><span data-stu-id="1a17d-134">Consider the following points:</span></span>

- <span data-ttu-id="1a17d-135">Zijn de functies, eind punten, services en andere resources in uw implementatie beschikbaar op de doel implementatie locaties?</span><span class="sxs-lookup"><span data-stu-id="1a17d-135">Are the functions, endpoints, services, and other resources in your deployment available in the target deployment locations?</span></span>
- <span data-ttu-id="1a17d-136">Zijn er configuratie-artefacten opgeslagen op locaties die toegankelijk zijn voor verschillende Clouds?</span><span class="sxs-lookup"><span data-stu-id="1a17d-136">Are configuration artifacts stored in locations that are accessible across clouds?</span></span>
- <span data-ttu-id="1a17d-137">Werken de implementatie parameters in alle doel omgevingen?</span><span class="sxs-lookup"><span data-stu-id="1a17d-137">Will deployment parameters work in all the target environments?</span></span>
- <span data-ttu-id="1a17d-138">Zijn er resource-specifieke eigenschappen beschikbaar in alle doel-Clouds?</span><span class="sxs-lookup"><span data-stu-id="1a17d-138">Are resource-specific properties available in all target clouds?</span></span>

<span data-ttu-id="1a17d-139">Zie [Azure Resource Manager sjablonen voor Cloud consistentie ontwikkelen](https://docs.microsoft.com/azure/azure-resource-manager/templates-cloud-consistency)voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="1a17d-139">For more information, see [Develop Azure Resource Manager templates for cloud consistency](https://docs.microsoft.com/azure/azure-resource-manager/templates-cloud-consistency).</span></span>

<span data-ttu-id="1a17d-140">Houd ook rekening met de volgende punten wanneer u bepaalt hoe u dit patroon wilt implementeren:</span><span class="sxs-lookup"><span data-stu-id="1a17d-140">In addition, consider the following points when deciding how to implement this pattern:</span></span>

### <a name="scalability"></a><span data-ttu-id="1a17d-141">Schaalbaarheid</span><span class="sxs-lookup"><span data-stu-id="1a17d-141">Scalability</span></span>

<span data-ttu-id="1a17d-142">Implementatie automatiserings systemen zijn het belangrijkste besturings punt in de DevOps-patronen.</span><span class="sxs-lookup"><span data-stu-id="1a17d-142">Deployment automation systems are the key control point in the DevOps Patterns.</span></span> <span data-ttu-id="1a17d-143">Implementaties kunnen variëren.</span><span class="sxs-lookup"><span data-stu-id="1a17d-143">Implementations can vary.</span></span> <span data-ttu-id="1a17d-144">De selectie van de juiste server grootte is afhankelijk van de grootte van de verwachte werk belasting.</span><span class="sxs-lookup"><span data-stu-id="1a17d-144">The selection of the correct server size depends on the size of the expected workload.</span></span> <span data-ttu-id="1a17d-145">Vm's kosten meer om te schalen dan containers.</span><span class="sxs-lookup"><span data-stu-id="1a17d-145">VMs cost more to scale than containers.</span></span> <span data-ttu-id="1a17d-146">Uw build-proces moet echter worden uitgevoerd met containers om containers te gebruiken voor schalen.</span><span class="sxs-lookup"><span data-stu-id="1a17d-146">To use containers for scaling, however, your build process must run with containers.</span></span>

### <a name="availability"></a><span data-ttu-id="1a17d-147">Beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="1a17d-147">Availability</span></span>

<span data-ttu-id="1a17d-148">Beschik baarheid in de context van de DevPattern houdt in dat status gegevens kunnen worden hersteld die zijn gekoppeld aan uw werk stroom, zoals test resultaten, code afhankelijkheden of andere artefacten.</span><span class="sxs-lookup"><span data-stu-id="1a17d-148">Availability in the context of the DevPattern means being able to recover any state information associated with your workflow, such as test results, code dependencies, or other artifacts.</span></span> <span data-ttu-id="1a17d-149">Overweeg twee algemene metrische gegevens als u uw beschikbaarheidsvereisten wilt beoordelen:</span><span class="sxs-lookup"><span data-stu-id="1a17d-149">To assess your availability requirements, consider two common metrics:</span></span>

- <span data-ttu-id="1a17d-150">Beoogde herstel tijd (RTO) geeft aan hoe lang u zonder systeem kunt gaan.</span><span class="sxs-lookup"><span data-stu-id="1a17d-150">Recovery Time Objective (RTO) specifies how long you can go without a system.</span></span>

- <span data-ttu-id="1a17d-151">Beoogd herstel punt (RPO) geeft aan hoeveel gegevens u kunt verliezen als een onderbreking in de service van invloed is op het systeem.</span><span class="sxs-lookup"><span data-stu-id="1a17d-151">Recovery Point Objective (RPO) indicates how much data you can afford to lose if a disruption in service affects the system.</span></span>

<span data-ttu-id="1a17d-152">In de praktijk, RTO en RPO is redundantie en back-up te impliceren.</span><span class="sxs-lookup"><span data-stu-id="1a17d-152">In practice, RTO, and RPO imply redundancy and backup.</span></span> <span data-ttu-id="1a17d-153">Op de wereld wijde Azure-Cloud is beschik baarheid geen vraag over het herstel van hardware. Dit is een onderdeel van Azure, maar u kunt de status van uw DevOps-systemen behouden.</span><span class="sxs-lookup"><span data-stu-id="1a17d-153">On the global Azure cloud, availability isn't a question of hardware recovery—that's part of Azure—but rather ensuring you maintain the state of your DevOps systems.</span></span> <span data-ttu-id="1a17d-154">Op Azure Stack hub is het mogelijk dat het herstel van hardware wordt overwogen.</span><span class="sxs-lookup"><span data-stu-id="1a17d-154">On Azure Stack Hub, hardware recovery may be a consideration.</span></span>

<span data-ttu-id="1a17d-155">Een andere belang rijke overweging bij het ontwerpen van het systeem dat wordt gebruikt voor implementatie automatisering is toegangs beheer en het juiste beheer van de benodigde rechten voor het implementeren van services in Cloud omgevingen.</span><span class="sxs-lookup"><span data-stu-id="1a17d-155">Another major consideration when designing the system used for deployment automation is access control and the proper management of the rights needed to deploy services to cloud environments.</span></span> <span data-ttu-id="1a17d-156">Welke rechten zijn er nodig om implementaties te maken, te verwijderen of te wijzigen?</span><span class="sxs-lookup"><span data-stu-id="1a17d-156">What rights are needed to create, delete, or modify deployments?</span></span> <span data-ttu-id="1a17d-157">Zo is bijvoorbeeld één set rechten vereist voor het maken van een resource groep in Azure en een andere voor het implementeren van services in de resource groep.</span><span class="sxs-lookup"><span data-stu-id="1a17d-157">For example, one set of rights is typically required to create a resource group in Azure and another to deploy services in the resource group.</span></span>

### <a name="manageability"></a><span data-ttu-id="1a17d-158">Beheerbaarheid</span><span class="sxs-lookup"><span data-stu-id="1a17d-158">Manageability</span></span>

<span data-ttu-id="1a17d-159">Het ontwerp van elk systeem op basis van het DevOps-patroon moet rekening houden met automatisering, logboek registratie en waarschuwingen voor elke service in de Port Folio.</span><span class="sxs-lookup"><span data-stu-id="1a17d-159">The design of any system based on the DevOps pattern must consider automation, logging, and alerting for each service across the portfolio.</span></span> <span data-ttu-id="1a17d-160">Gebruik gedeelde services, een toepassings team of beide, en houd ook het beveiligings beleid en governance bij.</span><span class="sxs-lookup"><span data-stu-id="1a17d-160">Use shared services, an application team, or both, and track security policies and governance as well.</span></span>

<span data-ttu-id="1a17d-161">Implementeer productie omgevingen en ontwikkel-en test omgevingen in afzonderlijke resource groepen op Azure of Azure Stack hub.</span><span class="sxs-lookup"><span data-stu-id="1a17d-161">Deploy production environments and development/test environments in separate resource groups on Azure or Azure Stack Hub.</span></span> <span data-ttu-id="1a17d-162">Vervolgens kunt u de resources van elke omgeving bewaken en de facturerings kosten per resource groep totaliseren.</span><span class="sxs-lookup"><span data-stu-id="1a17d-162">Then you can monitor each environment's resources and roll up billing costs by resource group.</span></span> <span data-ttu-id="1a17d-163">U kunt ook resources als een set verwijderen. Dit is handig voor test implementaties.</span><span class="sxs-lookup"><span data-stu-id="1a17d-163">You can also delete resources as a set, which is useful for test deployments.</span></span>

## <a name="when-to-use-this-pattern"></a><span data-ttu-id="1a17d-164">Wanneer dit patroon gebruiken</span><span class="sxs-lookup"><span data-stu-id="1a17d-164">When to use this pattern</span></span>

<span data-ttu-id="1a17d-165">Gebruik dit patroon als:</span><span class="sxs-lookup"><span data-stu-id="1a17d-165">Use this pattern if:</span></span>

- <span data-ttu-id="1a17d-166">U kunt code ontwikkelen in één omgeving die voldoet aan de behoeften van uw ontwikkel aars en implementeren in een omgeving die specifiek is voor uw oplossing, waar het lastig kan zijn om nieuwe code te ontwikkelen.</span><span class="sxs-lookup"><span data-stu-id="1a17d-166">You can develop code in one environment that meets the needs of your developers, and deploy to an environment specific to your solution where it may be difficult to develop new code.</span></span>
- <span data-ttu-id="1a17d-167">U kunt de code en hulpprogram ma's van uw ontwikkel aars gebruiken, zolang ze de continue integratie en continue levering van het proces in het DevOps-patroon kunnen volgen.</span><span class="sxs-lookup"><span data-stu-id="1a17d-167">You can use the code and tools your developers would like, as long as they're able to follow the continuous integration and continuous delivery process in the DevOps Pattern.</span></span>

<span data-ttu-id="1a17d-168">Dit patroon wordt niet aanbevolen voor het volgende:</span><span class="sxs-lookup"><span data-stu-id="1a17d-168">This pattern isn't recommended:</span></span>

- <span data-ttu-id="1a17d-169">Als u de infra structuur niet kunt automatiseren, dient u bronnen, configuratie-, identiteits-en beveiligings taken in te richten.</span><span class="sxs-lookup"><span data-stu-id="1a17d-169">If you can't automate infrastructure, provisioning resources, configuration, identity, and security tasks.</span></span>
- <span data-ttu-id="1a17d-170">Als teams geen toegang hebben tot hybride cloud resources om een continue integratie/doorlopende ontwikkeling (CI/CD)-benadering te implementeren.</span><span class="sxs-lookup"><span data-stu-id="1a17d-170">If teams don't have access to hybrid cloud resources to implement a Continuous Integration/Continuous Development (CI/CD) approach.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1a17d-171">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1a17d-171">Next steps</span></span>

<span data-ttu-id="1a17d-172">Voor meer informatie over de onderwerpen die in dit artikel worden geïntroduceerd:</span><span class="sxs-lookup"><span data-stu-id="1a17d-172">To learn more about topics introduced in this article:</span></span>

- <span data-ttu-id="1a17d-173">Raadpleeg de [documentatie van Azure DevOps](/azure/devops) voor meer informatie over Azure DevOps en gerelateerde hulpprogram ma's, waaronder Azure opslag plaatsen en Azure-pijp lijnen.</span><span class="sxs-lookup"><span data-stu-id="1a17d-173">See the [Azure DevOps documentation](/azure/devops) to learn more about Azure DevOps and related tools, including Azure Repos, and Azure Pipelines.</span></span>
- <span data-ttu-id="1a17d-174">Bekijk de [Azure stack-familie van producten en oplossingen](/azure-stack) voor meer informatie over de volledige Port Folio van producten en oplossingen.</span><span class="sxs-lookup"><span data-stu-id="1a17d-174">See the [Azure Stack family of products and solutions](/azure-stack) to learn more about the entire portfolio of products and solutions.</span></span>

<span data-ttu-id="1a17d-175">Wanneer u klaar bent om het voor beeld van de oplossing te testen, gaat u verder met de [implementatie handleiding voor hybride CI/cd-oplossingen van DevOps](https://aka.ms/hybriddevopsdeploy).</span><span class="sxs-lookup"><span data-stu-id="1a17d-175">When you're ready to test the solution example, continue with the [DevOps hybrid CI/CD solution deployment guide](https://aka.ms/hybriddevopsdeploy).</span></span> <span data-ttu-id="1a17d-176">De implementatie handleiding bevat stapsgewijze instructies voor het implementeren en testen van de onderdelen.</span><span class="sxs-lookup"><span data-stu-id="1a17d-176">The deployment guide provides step-by-step instructions for deploying and testing its components.</span></span> <span data-ttu-id="1a17d-177">U leert hoe u een app implementeert in Azure en Azure Stack hub met behulp van een pipeline met hybride doorlopende integratie/continue levering (CI/CD).</span><span class="sxs-lookup"><span data-stu-id="1a17d-177">You learn how to deploy an app to Azure and Azure Stack Hub using a hybrid continuous integration/continuous delivery (CI/CD) pipeline.</span></span>