---
title: Canaux de données de communication à distance holographiques personnalisés
description: Les canaux de données personnalisés peuvent être utilisés pour envoyer des données utilisateur sur la connexion de communication à distance holographique déjà établie.
author: NPohl-MSFT
ms.author: nopohl
ms.date: 08/01/2019
ms.topic: article
keywords: HoloLens, communication à distance, communication à distance holographique
ms.openlocfilehash: 9f7f20023d496412b331606e03d0c5110bb4864f
ms.sourcegitcommit: ca949efe0279995a376750d89e23d7123eb44846
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68718083"
---
# <a name="custom-holographic-remoting-data-channels"></a><span data-ttu-id="f4394-104">Canaux de données de communication à distance holographiques personnalisés</span><span class="sxs-lookup"><span data-stu-id="f4394-104">Custom Holographic Remoting data channels</span></span>

>[!NOTE]
><span data-ttu-id="f4394-105">Ce guide est spécifique à la communication à distance holographique sur HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="f4394-105">This guidance is specific to Holographic Remoting on HoloLens 2.</span></span>

<span data-ttu-id="f4394-106">Utilisez des canaux de données personnalisés pour envoyer des données personnalisées via une connexion de communication à distance établie.</span><span class="sxs-lookup"><span data-stu-id="f4394-106">Use custom data channels to send custom data over an established remoting connection.</span></span>

>[!IMPORTANT]
><span data-ttu-id="f4394-107">Les canaux de données personnalisés requièrent une application hôte personnalisée et une application de lecteur personnalisée, car elle permet la communication entre les deux applications personnalisées.</span><span class="sxs-lookup"><span data-stu-id="f4394-107">Custom data channels require a custom host app and a custom player app, as it allows for communication between the two custom apps.</span></span>

>[!TIP]
><span data-ttu-id="f4394-108">Un exemple de ping-pong simple se trouve dans les exemples d’hôtes et de lecteurs à l’intérieur du [référentiel GitHub des exemples de communication à distance holographique](https://github.com/microsoft/MixedReality-HolographicRemoting-Samples).</span><span class="sxs-lookup"><span data-stu-id="f4394-108">A simple ping-pong example can be found in the host and player samples inside the [Holographic Remoting samples github repository](https://github.com/microsoft/MixedReality-HolographicRemoting-Samples).</span></span> <span data-ttu-id="f4394-109">Supprimez ```#define ENABLE_CUSTOM_DATA_CHANNEL_SAMPLE``` les marques de commentaire dans les fichiers SampleHostMain. h/SamplePlayerMain. h pour activer l’exemple de code.</span><span class="sxs-lookup"><span data-stu-id="f4394-109">Uncomment ```#define ENABLE_CUSTOM_DATA_CHANNEL_SAMPLE``` inside the SampleHostMain.h / SamplePlayerMain.h files to enable the sample code.</span></span>


# <a name="create-a-custom-data-channel"></a><span data-ttu-id="f4394-110">Créer un canal de données personnalisé</span><span class="sxs-lookup"><span data-stu-id="f4394-110">Create a custom data channel</span></span>


<span data-ttu-id="f4394-111">Pour créer un canal de données personnalisé, les champs suivants sont requis:</span><span class="sxs-lookup"><span data-stu-id="f4394-111">To create a custom data channel, the following fields are required:</span></span>
```cpp
std::recursive_mutex m_customDataChannelLock;
winrt::Microsoft::Holographic::AppRemoting::IDataChannel m_customDataChannel = nullptr;
winrt::Microsoft::Holographic::AppRemoting::IDataChannel::OnDataReceived_revoker m_customChannelDataReceivedEventRevoker;
winrt::Microsoft::Holographic::AppRemoting::IDataChannel::OnClosed_revoker m_customChannelClosedEventRevoker;
```

<span data-ttu-id="f4394-112">Une fois la connexion établie, la création de nouveaux canaux de données peut être lancée du côté hôte et/ou du côté joueur.</span><span class="sxs-lookup"><span data-stu-id="f4394-112">After a connection was successfully established, the creation of new data channels can be initiated from either the host side and/or the player side.</span></span> <span data-ttu-id="f4394-113">RemoteContext et PlayerContext fournissent toutes les deux une ```CreateDataChannel()``` méthode pour effectuer cette opération.</span><span class="sxs-lookup"><span data-stu-id="f4394-113">Both the RemoteContext and the PlayerContext provide a ```CreateDataChannel()``` method to do this.</span></span> <span data-ttu-id="f4394-114">Le premier paramètre est l’ID de canal utilisé pour identifier le canal de données dans les opérations susequent.</span><span class="sxs-lookup"><span data-stu-id="f4394-114">The first parameter is the channel ID which is used to identify the data channel in susequent operations.</span></span> <span data-ttu-id="f4394-115">Le deuxième paramètre est la priorité qui spécifie la priorité avec laquelle les données de ce canal sont transférées de l’autre côté.</span><span class="sxs-lookup"><span data-stu-id="f4394-115">The second paramter is the priority which specifies the priority with which data of this channel is transfered to the other side.</span></span> <span data-ttu-id="f4394-116">La plage valide pour les ID de canal est comprise entre 0 et 63 inclus pour le côté hôte et 64 jusqu’à 127 inclus pour le côté joueur.</span><span class="sxs-lookup"><span data-stu-id="f4394-116">The valid range for channel IDs is 0 up to and including 63 for the host side and 64 up to and including 127 for the player side.</span></span> <span data-ttu-id="f4394-117">Les priorités valides ```Medium``` sont ```High``` ```Low```, ou (des deux côtés).</span><span class="sxs-lookup"><span data-stu-id="f4394-117">Valid priorities are ```Low```, ```Medium``` or ```High``` (on both sides).</span></span>

<span data-ttu-id="f4394-118">Pour initier la création d’un canal de données côté **hôte** :</span><span class="sxs-lookup"><span data-stu-id="f4394-118">To initiate the creation of a data channel on the **host** side:</span></span>
```cpp
// Valid channel ids for channels created on the host side are 0 up to and including 63
m_remoteContext.CreateDataChannel(0, DataChannelPriority::Low);
```

<span data-ttu-id="f4394-119">Pour initier la création d’un canal de données côté **joueur** :</span><span class="sxs-lookup"><span data-stu-id="f4394-119">To initiate the creation of a data channel on the **player** side:</span></span>
```cpp
// Valid channel ids for channels created on the player side are 64 up to and including 127
m_playerContext.CreateDataChannel(64, DataChannelPriority::Low);
```

>[!NOTE]
><span data-ttu-id="f4394-120">Pour créer un canal de données personnalisé, un seul côté (hôte ou lecteur) doit appeler la ```CreateDataChannel``` méthode.</span><span class="sxs-lookup"><span data-stu-id="f4394-120">To create a new custom data channel, only one side (either host or player) needs to call the ```CreateDataChannel``` method.</span></span>

## <a name="handling-custom-data-channel-events"></a><span data-ttu-id="f4394-121">Gestion des événements de canal de données personnalisé</span><span class="sxs-lookup"><span data-stu-id="f4394-121">Handling custom data channel events</span></span>

<span data-ttu-id="f4394-122">Pour établir un canal de données personnalisé, ```OnDataChannelCreated``` l’événement doit être géré (à la fois sur le joueur et le côté hôte).</span><span class="sxs-lookup"><span data-stu-id="f4394-122">To establish a custom data channel, the ```OnDataChannelCreated``` event needs to be handled (on both the player and the host side).</span></span> <span data-ttu-id="f4394-123">Il se déclenche lorsqu’un canal de données utilisateur a été créé par chaque côté et fournit ```IDataChannel``` un objet, qui peut être utilisé pour envoyer et recevoir des données sur ce canal.</span><span class="sxs-lookup"><span data-stu-id="f4394-123">It triggers when a user data channel has been created by either side and provides a ```IDataChannel``` object, which can be used to send and receive data over this channel.</span></span>

<span data-ttu-id="f4394-124">Pour inscrire un écouteur sur l' ```OnDataChannelCreated``` événement:</span><span class="sxs-lookup"><span data-stu-id="f4394-124">To register a listener on the ```OnDataChannelCreated``` event:</span></span>
```cpp
m_onDataChannelCreatedEventRevoker = m_remoteContext.OnDataChannelCreated(winrt::auto_revoke,
    [this](const IDataChannel& dataChannel, uint8_t channelId)
    {
        std::lock_guard lock(m_customDataChannelLock);
        m_customDataChannel = dataChannel;

        // Register to OnDataReceived and OnClosed event of the data channel here, see below...
    });
```

<span data-ttu-id="f4394-125">Pour être informé de la réception des données, inscrivez- ```OnDataReceived``` vous à l' ```IDataChannel``` événement sur l’objet ```OnDataChannelCreated``` fourni par le gestionnaire.</span><span class="sxs-lookup"><span data-stu-id="f4394-125">To get notified when data is received, register to the ```OnDataReceived``` event on the ```IDataChannel``` object provided by the ```OnDataChannelCreated``` handler.</span></span> <span data-ttu-id="f4394-126">Inscrivez-vous ```OnClosed``` à l’événement pour être informé de la fermeture du canal de données.</span><span class="sxs-lookup"><span data-stu-id="f4394-126">Register to the ```OnClosed``` event, to get notified when the data channel has been closed.</span></span>

```cpp
m_customChannelDataReceivedEventRevoker = m_customDataChannel.OnDataReceived(winrt::auto_revoke, 
    [this]()
    {
        // React on data received via the custom data channel here.
    });

m_customChannelClosedEventRevoker = m_customDataChannel.OnClosed(winrt::auto_revoke,
    [this]()
    {
        // React on data channel closed here.

        std::lock_guard lock(m_customDataChannelLock);
        if (m_customDataChannel)
        {
            m_customDataChannel = nullptr;
        }
    });
```

## <a name="sending-data"></a><span data-ttu-id="f4394-127">Envoi de données</span><span class="sxs-lookup"><span data-stu-id="f4394-127">Sending data</span></span>

<span data-ttu-id="f4394-128">Pour envoyer des données sur un canal de données personnalisé, ```IDataChannel::SendData()``` utilisez la méthode.</span><span class="sxs-lookup"><span data-stu-id="f4394-128">To send data over a custom data channel, use the ```IDataChannel::SendData()``` method.</span></span> <span data-ttu-id="f4394-129">Le premier paramètre est un ```winrt::array_view<const uint8_t>``` pour les données qui doivent être envoyées.</span><span class="sxs-lookup"><span data-stu-id="f4394-129">The first paramter is a ```winrt::array_view<const uint8_t>``` to the data that should be send.</span></span> <span data-ttu-id="f4394-130">Le deuxième paramètre spécifie si les données doivent être renvoyées, jusqu’à ce que l’autre côté accuse réception de la réception.</span><span class="sxs-lookup"><span data-stu-id="f4394-130">The second parameter specifies wheter the data should be resend, until the other side acknowledge the reception.</span></span> 

>[!IMPORTANT]
><span data-ttu-id="f4394-131">En cas de mauvaises conditions de réseau, le même paquet de données peut arriver plusieurs fois.</span><span class="sxs-lookup"><span data-stu-id="f4394-131">In case of bad network conditions, the same data packet might arrive more than once.</span></span> <span data-ttu-id="f4394-132">Le code de réception doit être en mesure de gérer cette situation.</span><span class="sxs-lookup"><span data-stu-id="f4394-132">The receiving code must be able to handle this situation.</span></span>

```cpp
uint8_t data[] = {1};
m_customDataChannel.SendData(data, true);
```

## <a name="closing-a-custom-data-channel"></a><span data-ttu-id="f4394-133">Fermeture d’un canal de données personnalisé</span><span class="sxs-lookup"><span data-stu-id="f4394-133">Closing a custom data channel</span></span>

<span data-ttu-id="f4394-134">Pour fermer un canal de données personnalisé, utilisez ```IDataChannel::Close()``` la méthode.</span><span class="sxs-lookup"><span data-stu-id="f4394-134">To close a custom data channel, use the ```IDataChannel::Close()``` method.</span></span> <span data-ttu-id="f4394-135">Les deux côtés sont avertis par l' ```OnClosed``` événement une fois que le canal de données personnalisé a été fermé.</span><span class="sxs-lookup"><span data-stu-id="f4394-135">Both sides will be notified by the ```OnClosed``` event once the custom data channel has been closed.</span></span>

```cpp
m_customDataChannel.Close();
```

## <a name="see-also"></a><span data-ttu-id="f4394-136">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="f4394-136">See Also</span></span>
* [<span data-ttu-id="f4394-137">Écriture d’une application hôte de communication à distance holographique</span><span class="sxs-lookup"><span data-stu-id="f4394-137">Writing a Holographic Remoting host app</span></span>](holographic-remoting-create-host.md)
* [<span data-ttu-id="f4394-138">Écriture d’une application de lecteur de communication à distance holographique personnalisée</span><span class="sxs-lookup"><span data-stu-id="f4394-138">Writing a custom Holographic Remoting player app</span></span>](holographic-remoting-create-player.md)
* [<span data-ttu-id="f4394-139">Résolution des problèmes et limitations de la communication à distance holographique</span><span class="sxs-lookup"><span data-stu-id="f4394-139">Holographic Remoting troubleshooting and limitations</span></span>](holographic-remoting-troubleshooting.md)
* [<span data-ttu-id="f4394-140">Termes du contrat de licence du logiciel de communication à distance holographique</span><span class="sxs-lookup"><span data-stu-id="f4394-140">Holographic Remoting software license terms</span></span>](https://docs.microsoft.com/en-us/legal/mixed-reality/microsoft-holographic-remoting-software-license-terms)
* [<span data-ttu-id="f4394-141">Déclaration de confidentialité Microsoft</span><span class="sxs-lookup"><span data-stu-id="f4394-141">Microsoft Privacy Statement</span></span>](https://go.microsoft.com/fwlink/?LinkId=521839)