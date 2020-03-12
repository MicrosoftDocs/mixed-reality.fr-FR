---
title: Canaux de données de communication à distance holographiques personnalisés
description: Les canaux de données personnalisés peuvent être utilisés pour envoyer des données utilisateur sur la connexion de communication à distance holographique déjà établie.
author: FlorianBagarMicrosoft
ms.author: flbagar
ms.date: 03/11/2020
ms.topic: article
keywords: HoloLens, communication à distance, communication à distance holographique
ms.openlocfilehash: 8bfa19b7af0f3429130aabf70d9d11083bc56a52
ms.sourcegitcommit: 0a1af2224c9cbb34591b6cb01159b60b37dfff0c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/11/2020
ms.locfileid: "79092296"
---
# <a name="custom-holographic-remoting-data-channels"></a><span data-ttu-id="f5a26-104">Canaux de données de communication à distance holographiques personnalisés</span><span class="sxs-lookup"><span data-stu-id="f5a26-104">Custom Holographic Remoting data channels</span></span>

>[!NOTE]
><span data-ttu-id="f5a26-105">Ce guide est spécifique à la communication à distance holographique sur HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="f5a26-105">This guidance is specific to Holographic Remoting on HoloLens 2.</span></span>

<span data-ttu-id="f5a26-106">Utilisez des canaux de données personnalisés pour envoyer des données personnalisées via une connexion de communication à distance établie.</span><span class="sxs-lookup"><span data-stu-id="f5a26-106">Use custom data channels to send custom data over an established remoting connection.</span></span>

>[!IMPORTANT]
><span data-ttu-id="f5a26-107">Les canaux de données personnalisés requièrent une application distante personnalisée et une application de lecteur personnalisée, car elle permet la communication entre les deux applications personnalisées.</span><span class="sxs-lookup"><span data-stu-id="f5a26-107">Custom data channels require a custom remote app and a custom player app, as it allows for communication between the two custom apps.</span></span>

>[!TIP]
><span data-ttu-id="f5a26-108">Un simple exemple de ping-pong se trouve dans les exemples Remote et Player à l’intérieur du [référentiel GitHub des exemples de communication](https://github.com/microsoft/MixedReality-HolographicRemoting-Samples)à distance holographique.</span><span class="sxs-lookup"><span data-stu-id="f5a26-108">A simple ping-pong example can be found in the remote and player samples inside the [Holographic Remoting samples github repository](https://github.com/microsoft/MixedReality-HolographicRemoting-Samples).</span></span> <span data-ttu-id="f5a26-109">Supprimez les marques de commentaire ```#define ENABLE_CUSTOM_DATA_CHANNEL_SAMPLE``` dans les fichiers SampleRemoteMain. h/SamplePlayerMain. h pour activer l’exemple de code.</span><span class="sxs-lookup"><span data-stu-id="f5a26-109">Uncomment ```#define ENABLE_CUSTOM_DATA_CHANNEL_SAMPLE``` inside the SampleRemoteMain.h / SamplePlayerMain.h files to enable the sample code.</span></span>


## <a name="create-a-custom-data-channel"></a><span data-ttu-id="f5a26-110">Créer un canal de données personnalisé</span><span class="sxs-lookup"><span data-stu-id="f5a26-110">Create a custom data channel</span></span>


<span data-ttu-id="f5a26-111">Pour créer un canal de données personnalisé, les champs suivants sont requis :</span><span class="sxs-lookup"><span data-stu-id="f5a26-111">To create a custom data channel, the following fields are required:</span></span>
```cpp
std::recursive_mutex m_customDataChannelLock;
winrt::Microsoft::Holographic::AppRemoting::IDataChannel m_customDataChannel = nullptr;
winrt::Microsoft::Holographic::AppRemoting::IDataChannel::OnDataReceived_revoker m_customChannelDataReceivedEventRevoker;
winrt::Microsoft::Holographic::AppRemoting::IDataChannel::OnClosed_revoker m_customChannelClosedEventRevoker;
```

<span data-ttu-id="f5a26-112">Une fois la connexion établie, la création de nouveaux canaux de données peut être lancée à partir du côté distant et/ou du côté joueur.</span><span class="sxs-lookup"><span data-stu-id="f5a26-112">After a connection was successfully established, the creation of new data channels can be initiated from either the remote side and/or the player side.</span></span> <span data-ttu-id="f5a26-113">Les RemoteContext et PlayerContext fournissent une méthode ```CreateDataChannel()``` pour effectuer cette opération.</span><span class="sxs-lookup"><span data-stu-id="f5a26-113">Both the RemoteContext and the PlayerContext provide a ```CreateDataChannel()``` method to do this.</span></span> <span data-ttu-id="f5a26-114">Le premier paramètre est l’ID de canal qui est utilisé pour identifier le canal de données dans les opérations suivantes.</span><span class="sxs-lookup"><span data-stu-id="f5a26-114">The first parameter is the channel ID which is used to identify the data channel in subsequent operations.</span></span> <span data-ttu-id="f5a26-115">Le deuxième paramètre est la priorité qui spécifie la priorité avec laquelle les données de ce canal sont transférées de l’autre côté.</span><span class="sxs-lookup"><span data-stu-id="f5a26-115">The second parameter is the priority which specifies the priority with which data of this channel is transferred to the other side.</span></span> <span data-ttu-id="f5a26-116">La plage valide pour les ID de canal est comprise entre 0 et 63 inclus pour le côté distant et 64 jusqu’à 127 inclus pour le côté joueur.</span><span class="sxs-lookup"><span data-stu-id="f5a26-116">The valid range for channel IDs is 0 up to and including 63 for the remote side and 64 up to and including 127 for the player side.</span></span> <span data-ttu-id="f5a26-117">Les priorités valides sont ```Low```, ```Medium``` ou ```High``` (des deux côtés).</span><span class="sxs-lookup"><span data-stu-id="f5a26-117">Valid priorities are ```Low```, ```Medium``` or ```High``` (on both sides).</span></span>

<span data-ttu-id="f5a26-118">Pour initier la création d’un canal de données côté **distant** :</span><span class="sxs-lookup"><span data-stu-id="f5a26-118">To initiate the creation of a data channel on the **remote** side:</span></span>
```cpp
// Valid channel ids for channels created on the remote side are 0 up to and including 63
m_remoteContext.CreateDataChannel(0, DataChannelPriority::Low);
```

<span data-ttu-id="f5a26-119">Pour initier la création d’un canal de données côté **joueur** :</span><span class="sxs-lookup"><span data-stu-id="f5a26-119">To initiate the creation of a data channel on the **player** side:</span></span>
```cpp
// Valid channel ids for channels created on the player side are 64 up to and including 127
m_playerContext.CreateDataChannel(64, DataChannelPriority::Low);
```

>[!NOTE]
><span data-ttu-id="f5a26-120">Pour créer un canal de données personnalisé, un seul côté (distant ou lecteur) doit appeler la méthode ```CreateDataChannel```.</span><span class="sxs-lookup"><span data-stu-id="f5a26-120">To create a new custom data channel, only one side (either remote or player) needs to call the ```CreateDataChannel``` method.</span></span>

## <a name="handling-custom-data-channel-events"></a><span data-ttu-id="f5a26-121">Gestion des événements de canal de données personnalisé</span><span class="sxs-lookup"><span data-stu-id="f5a26-121">Handling custom data channel events</span></span>

<span data-ttu-id="f5a26-122">Pour établir un canal de données personnalisé, l’événement ```OnDataChannelCreated``` doit être géré (à la fois sur le joueur et le côté distant).</span><span class="sxs-lookup"><span data-stu-id="f5a26-122">To establish a custom data channel, the ```OnDataChannelCreated``` event needs to be handled (on both the player and the remote side).</span></span> <span data-ttu-id="f5a26-123">Il se déclenche lorsqu’un canal de données utilisateur a été créé par chaque côté et fournit un objet ```IDataChannel```, qui peut être utilisé pour envoyer et recevoir des données sur ce canal.</span><span class="sxs-lookup"><span data-stu-id="f5a26-123">It triggers when a user data channel has been created by either side and provides a ```IDataChannel``` object, which can be used to send and receive data over this channel.</span></span>

<span data-ttu-id="f5a26-124">Pour inscrire un écouteur sur l’événement ```OnDataChannelCreated``` :</span><span class="sxs-lookup"><span data-stu-id="f5a26-124">To register a listener on the ```OnDataChannelCreated``` event:</span></span>
```cpp
m_onDataChannelCreatedEventRevoker = m_remoteContext.OnDataChannelCreated(winrt::auto_revoke,
    [this](const IDataChannel& dataChannel, uint8_t channelId)
    {
        std::lock_guard lock(m_customDataChannelLock);
        m_customDataChannel = dataChannel;

        // Register to OnDataReceived and OnClosed event of the data channel here, see below...
    });
```

<span data-ttu-id="f5a26-125">Pour être informé de la réception des données, inscrivez-vous à l’événement ```OnDataReceived``` sur l’objet ```IDataChannel``` fourni par le gestionnaire de ```OnDataChannelCreated```.</span><span class="sxs-lookup"><span data-stu-id="f5a26-125">To get notified when data is received, register to the ```OnDataReceived``` event on the ```IDataChannel``` object provided by the ```OnDataChannelCreated``` handler.</span></span> <span data-ttu-id="f5a26-126">Inscrivez-vous à l’événement ```OnClosed``` pour être informé lorsque le canal de données a été fermé.</span><span class="sxs-lookup"><span data-stu-id="f5a26-126">Register to the ```OnClosed``` event, to get notified when the data channel has been closed.</span></span>

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

## <a name="sending-data"></a><span data-ttu-id="f5a26-127">Envoi de données</span><span class="sxs-lookup"><span data-stu-id="f5a26-127">Sending data</span></span>

<span data-ttu-id="f5a26-128">Pour envoyer des données sur un canal de données personnalisé, utilisez la méthode ```IDataChannel::SendData()```.</span><span class="sxs-lookup"><span data-stu-id="f5a26-128">To send data over a custom data channel, use the ```IDataChannel::SendData()``` method.</span></span> <span data-ttu-id="f5a26-129">Le premier paramètre est un ```winrt::array_view<const uint8_t>``` des données qui doivent être envoyées.</span><span class="sxs-lookup"><span data-stu-id="f5a26-129">The first parameter is a ```winrt::array_view<const uint8_t>``` to the data that should be send.</span></span> <span data-ttu-id="f5a26-130">Le deuxième paramètre spécifie l’emplacement où les données doivent être renvoyées, jusqu’à ce que l’autre côté accuse réception de la réception.</span><span class="sxs-lookup"><span data-stu-id="f5a26-130">The second parameter specifies where the data should be resend, until the other side acknowledge the reception.</span></span> 

>[!IMPORTANT]
><span data-ttu-id="f5a26-131">En cas de mauvaises conditions de réseau, le même paquet de données peut arriver plusieurs fois.</span><span class="sxs-lookup"><span data-stu-id="f5a26-131">In case of bad network conditions, the same data packet might arrive more than once.</span></span> <span data-ttu-id="f5a26-132">Le code de réception doit être en mesure de gérer cette situation.</span><span class="sxs-lookup"><span data-stu-id="f5a26-132">The receiving code must be able to handle this situation.</span></span>

```cpp
uint8_t data[] = {1};
m_customDataChannel.SendData(data, true);
```

## <a name="closing-a-custom-data-channel"></a><span data-ttu-id="f5a26-133">Fermeture d’un canal de données personnalisé</span><span class="sxs-lookup"><span data-stu-id="f5a26-133">Closing a custom data channel</span></span>

<span data-ttu-id="f5a26-134">Pour fermer un canal de données personnalisé, utilisez la méthode ```IDataChannel::Close()```.</span><span class="sxs-lookup"><span data-stu-id="f5a26-134">To close a custom data channel, use the ```IDataChannel::Close()``` method.</span></span> <span data-ttu-id="f5a26-135">Les deux côtés sont avertis par l’événement ```OnClosed``` une fois que le canal de données personnalisé a été fermé.</span><span class="sxs-lookup"><span data-stu-id="f5a26-135">Both sides will be notified by the ```OnClosed``` event once the custom data channel has been closed.</span></span>

```cpp
m_customDataChannel.Close();
```

## <a name="see-also"></a><span data-ttu-id="f5a26-136">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="f5a26-136">See Also</span></span>
* [<span data-ttu-id="f5a26-137">Écriture d’une application distante de communication à distance holographique</span><span class="sxs-lookup"><span data-stu-id="f5a26-137">Writing a Holographic Remoting remote app</span></span>](holographic-remoting-create-host.md)
* [<span data-ttu-id="f5a26-138">Écriture d’une application de lecteur de communication à distance holographique personnalisée</span><span class="sxs-lookup"><span data-stu-id="f5a26-138">Writing a custom Holographic Remoting player app</span></span>](holographic-remoting-create-player.md)
* [<span data-ttu-id="f5a26-139">Résolution des problèmes et limitations de la communication à distance holographique</span><span class="sxs-lookup"><span data-stu-id="f5a26-139">Holographic Remoting troubleshooting and limitations</span></span>](holographic-remoting-troubleshooting.md)
* [<span data-ttu-id="f5a26-140">Termes du contrat de licence de la communication à distance holographique</span><span class="sxs-lookup"><span data-stu-id="f5a26-140">Holographic Remoting software license terms</span></span>](https://docs.microsoft.com//legal/mixed-reality/microsoft-holographic-remoting-software-license-terms)
* [<span data-ttu-id="f5a26-141">Déclaration de confidentialité Microsoft</span><span class="sxs-lookup"><span data-stu-id="f5a26-141">Microsoft Privacy Statement</span></span>](https://go.microsoft.com/fwlink/?LinkId=521839)
