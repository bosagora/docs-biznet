# NFT 메타데이터 표준

## 토큰 URI 구현

BizNet의 마켓플레이스가 ERC721 자산에 대한 오프체인 메타데이터를 가져올 수 있도록 하려면 NFT 계약에서 메타데이터를 찾을 수 있는 URI를 반환해야 합니다. 
이 URI를 찾기 위해 ERC721의 tokenURI 메소드와 ERC1155의 URI 메소드를 사용하여 NFT를 추적합니다. 계약에서 기능을 구현해야 합니다.

```

/**
 * @dev Returns an URI for a given token ID
 */
function tokenURI(uint256 _tokenId) public view returns (string) {
  return Strings.strConcat(
      baseTokenURI(),
      Strings.uint2str(_tokenId)
  );
}

```

계약의 tokenURI 함수는 HTTP 또는 IPFS URL을 반환해야 합니다. 쿼리할 때 이 URL은 토큰에 대한 메타데이터가 포함된 JSON 데이터 blob을 반환해야 합니다.

## 메타데이터 구조

BizNet의 마켓플레이스 는 [공식 ERC721 메타데이터 표준](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-721.md) 에 따라 구조화된 메타데이터를 지원합니다. 
또한 항목에 대한 여러 속성이 지원되어 BizeNet Marketplace에서 모든 정렬 및 필터링 기능을 제공합니다. 아래 메타데이터 구조를 통해 BizNet Marketplace는 NFT가 나타내는 자산에 대한 세부 정보를 읽고 표시할 수 있습니다.


```

{
    "name":"NFT Name",
    "description":"NFT Description",
    "image":"https://somedomain.com/pic/xxxx.jpg",
    "external_url":"https://originalsite.io/2",
    "attributes":[...]
}

```

이러한 각 속성의 작동 방식은 다음과 같습니다.

| 속성             | 설                                                                                                                                                         |
|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| name           | 항목의 이름입니다. 최대 200자입니다.                                                                                                                                    |
| description    | 사람이 읽을 수 있는 항목 설명입니다. 마크다운이 지원됩니다. 최대 500자입니다.                                                                                                            |
| image          | 항목의 이미지에 대한 URL입니다. 거의 모든 유형의 이미지가 될 수 있습니다. 350 x 350 이미지가 권장됩니다.                                                                                        |
| animation_url  | 항목에 대한 멀티미디어 첨부 파일의 URL입니다. 파일 확장자 GLTF, GLB, WEBM, MP4, M4V, OGV 및 OGG와 오디오 전용 확장자 MP3, WAV 및 OGA가 지원됩니다.                                                |
| animation_type | animation_url에서 제공하는 멀티미디어 첨부 파일 형식입니다. |
| external_url   | 이것은 마켓플레이스에서 자산 이미지 아래에 표시될 URL이며 사용자가 마켓플레이스를 떠나 사이트에서 항목을 볼 수 있도록 합니다.|
| attributes     | NFT의 세부 사항을 설명하는 항목의 속성입니다. (아래 배열 참조)|

### 속성
NFT 특성을 표시하려면 메타데이터에 다음 배열을 포함합니다.

```

{
    "attributes":[
        {
            "trait_type":"Rarity Class",
            "value":"Normal"
        },
        {
            "trait_type":"Type",
            "value":"Male"
        },
        {
            "trait_type":"Face",
            "value":"Mole"
        },
        {
            "trait_type":"Beard",
            "value":"Chinstrap"
        },
        {
            "display_type":"boost_number",
            "trait_type":"Power",
            "value":"Power"
        },
        {
            "display_type":"boost_percentage",
            "trait_type":"Health Increase",
            "value":"20"
        },
        {
            "display_type":"number",
            "trait_type":"Generation",
            "value":"3"
        }
    ]
}

```
다음 `trait_type` 은 특성의 이름이고, `value`는 특성의 값이며, `display_type`는 숫자 값을 표시하는 방법을 나타내는 필드입니다.  
`display_type` 대해서는 `value`가 문자열일 경우에는 걱정할 필요가 없습니다.  
속성에 포함된 모든 특성은 에 표시됩니다 Attribute. 특정 트레이트에 대한 속성 을 원하지 않는 경우 `trait_type`을 사용하지 않고 `value`만을 포함하면 일반 속성으로 설정됩니다.  

#### 숫자 특성  
3가지 지원 옵션이 있습니다.  
display_type: `number` - 순수한 숫자로 값  
display_type: `boost_number` - 더하기 또는 빼기 기호로 숫자를 표시할 수 있습니다.  
display_type: `boost_percentage` - `boost_number`와 유사하지만 숫자 뒤에 퍼센트 기호를 표시합니다.  

#### 날짜  
마켓플레이스에서는 날짜 특성도 지원합니다. UNIX 타임스탬프를 값으로 전달합니다.
```

   {
      "display_type": "date", 
      "trait_type": "birthday", 
      "value": 1608490000
    }
    
```