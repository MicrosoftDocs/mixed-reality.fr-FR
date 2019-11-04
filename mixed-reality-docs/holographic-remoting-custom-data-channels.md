---
title: Canaux de données de communication à distance holographiques personnalisés
description: Les canaux de données personnalisés peuvent être utilisés pour envoyer des données utilisateur sur la connexion de communication à distance holographique déjà établie.
author: NPohl-MSFT
ms.author: nopohl
ms.date: 10/21/2019
ms.topic: article
keywords: HoloLens, communication à distance, communication à distance holographique
ms.openlocfilehash: a862fa52695c7bfb94b58c6c0b85606a112835da
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73434276"
---
# <a name="custom-holographic-remoting-data-channels"></a>Canaux de données de communication à distance holographiques personnalisés

>[!NOTE]
>Ce guide est spécifique à la communication à distance holographique sur HoloLens 2.

Utilisez des canaux de données personnalisés pour envoyer des données personnalisées via une connexion de communication à distance établie.

>[!IMPORTANT]
>Les canaux de données personnalisés requièrent une application hôte personnalisée et une application de lecteur personnalisée, car elle permet la communication entre les deux applications personnalisées.

>[!TIP]
>Un exemple de ping-pong simple se trouve dans les exemples d’hôtes et de lecteurs à l’intérieur du [référentiel GitHub des exemples de communication à distance holographique](https://github.com/microsoft/MixedReality-HolographicRemoting-Samples). Supprimez les marques de commentaire ```#define ENABLE_CUSTOM_DATA_CHANNEL_SAMPLE``` dans les fichiers SampleHostMain. h/SamplePlayerMain. h pour activer l’exemple de code.


## <a name="create-a-custom-data-channel"></a>Créer un canal de données personnalisé


Pour créer un canal de données personnalisé, les champs suivants sont requis :
```cpp
std::recursive_mutex m_customDataChannelLock;
winrt::Microsoft::Holographic::AppRemoting::IDataChannel m_customDataChannel = nullptr;
winrt::Microsoft::Holographic::AppRemoting::IDataChannel::OnDataReceived_revoker m_customChannelDataReceivedEventRevoker;
winrt::Microsoft::Holographic::AppRemoting::IDataChannel::OnClosed_revoker m_customChannelClosedEventRevoker;
```

Une fois la connexion établie, la création de nouveaux canaux de données peut être lancée du côté hôte et/ou du côté joueur. Les RemoteContext et PlayerContext fournissent une méthode ```CreateDataChannel()``` pour effectuer cette opération. Le premier paramètre est l’ID de canal utilisé pour identifier le canal de données dans les opérations susequent. Le deuxième paramètre est la priorité qui spécifie la priorité avec laquelle les données de ce canal sont transférées de l’autre côté. La plage valide pour les ID de canal est comprise entre 0 et 63 inclus pour le côté hôte et 64 jusqu’à 127 inclus pour le côté joueur. Les priorités valides sont ```Low```, ```Medium``` ou ```High``` (des deux côtés).

Pour initier la création d’un canal de données côté **hôte** :
```cpp
// Valid channel ids for channels created on the host side are 0 up to and including 63
m_remoteContext.CreateDataChannel(0, DataChannelPriority::Low);
```

Pour initier la création d’un canal de données côté **joueur** :
```cpp
// Valid channel ids for channels created on the player side are 64 up to and including 127
m_playerContext.CreateDataChannel(64, DataChannelPriority::Low);
```

>[!NOTE]
>Pour créer un canal de données personnalisé, un seul côté (hôte ou lecteur) doit appeler la méthode ```CreateDataChannel```.

## <a name="handling-custom-data-channel-events"></a>Gestion des événements de canal de données personnalisé

Pour établir un canal de données personnalisé, l’événement ```OnDataChannelCreated``` doit être géré (à la fois sur le joueur et le côté hôte). Il se déclenche lorsqu’un canal de données utilisateur a été créé par chaque côté et fournit un objet ```IDataChannel```, qui peut être utilisé pour envoyer et recevoir des données sur ce canal.

Pour inscrire un écouteur sur l’événement ```OnDataChannelCreated``` :
```cpp
m_onDataChannelCreatedEventRevoker = m_remoteContext.OnDataChannelCreated(winrt::auto_revoke,
    [this](const IDataChannel& dataChannel, uint8_t channelId)
    {
        std::lock_guard lock(m_customDataChannelLock);
        m_customDataChannel = dataChannel;

        // Register to OnDataReceived and OnClosed event of the data channel here, see below...
    });
```

Pour être informé de la réception des données, inscrivez-vous à l’événement ```OnDataReceived``` sur l’objet ```IDataChannel``` fourni par le gestionnaire de ```OnDataChannelCreated```. Inscrivez-vous à l’événement ```OnClosed``` pour être informé lorsque le canal de données a été fermé.

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

## <a name="sending-data"></a>Envoi de données

Pour envoyer des données sur un canal de données personnalisé, utilisez la méthode ```IDataChannel::SendData()```. Le premier paramètre est un ```winrt::array_view<const uint8_t>``` des données qui doivent être envoyées. Le deuxième paramètre spécifie si les données doivent être renvoyées, jusqu’à ce que l’autre côté accuse réception de la réception. 

>[!IMPORTANT]
>En cas de mauvaises conditions de réseau, le même paquet de données peut arriver plusieurs fois. Le code de réception doit être en mesure de gérer cette situation.

```cpp
uint8_t data[] = {1};
m_customDataChannel.SendData(data, true);
```

## <a name="closing-a-custom-data-channel"></a>Fermeture d’un canal de données personnalisé

Pour fermer un canal de données personnalisé, utilisez la méthode ```IDataChannel::Close()```. Les deux côtés sont avertis par l’événement ```OnClosed``` une fois que le canal de données personnalisé a été fermé.

```cpp
m_customDataChannel.Close();
```

## <a name="see-also"></a>Articles associés
* [Écriture d’une application hôte de communication à distance holographique](holographic-remoting-create-host.md)
* [Écriture d’une application de lecteur de communication à distance holographique personnalisée](holographic-remoting-create-player.md)
* [Résolution des problèmes et limitations de la communication à distance holographique](holographic-remoting-troubleshooting.md)
* [Termes du contrat de licence de la communication à distance holographique](https://docs.microsoft.com//legal/mixed-reality/microsoft-holographic-remoting-software-license-terms)
* [Déclaration de confidentialité Microsoft](https://go.microsoft.com/fwlink/?LinkId=521839)
