# 검증가능하고 안전한 EOS 모바일 지갑 선택방법.

## HOST 변경기능이 있는가?

* EOS 에는 `nodeos` 라는 코인 데몬과 `keosd` 라는 지갑데몬이 존재함.
* EOS 블록체인에 원격으로 transaction 을 발생 시키려면 서버에 `nodeos` 가 실행되고 있어야함.
* 모바일 지갑에서 `nodeos`에 접근할때 꼭 해당 지갑에서 제공하는 서버가 아니고 다른 Host 에 붙였을 때도 모바일 지갑이 잘 동작해야, **악의적인 조작** 을 가하지 않았다는것을 검증 할 수 있음.

``` 
특정서버에서 import private key 요청을 받아 API 를 nodeos 로 보내서 정상동작하게 하고 추후에 private key 로 EOS를 탈취
특정서버에서 Unlock wallet password 요청을 받아 해당 권한으로 EOS 를 탈취
```

## 정상적인 API 가 호출되고 있는가?

* Network 패킷을 열어서 호출되는 API 주소가 정상적인지 확인해야함.
`nodeos`에 호출가능한 API 목록은 [여기](https://developers.eos.io/eosio-nodeos/reference) 서 확인 할 수 있음.

## 콜드월렛이 존재하는가?

* Cold wallet 은 off-line 환경에서 동작 가능한 지갑을 말함.
* EOS 에서 wallet 의 역할은 private key 를 안전하게 보관하고, 권한이 필요한 transaction 을 **sign** 할 수 있어야함. (`keosd` 의 역할)
* EOS 에서 제공하는 `keosd` 에 원격으로 접속해서 **sign** 기능을 하는 모바일 지갑은 지갑을 여는 password 가 원격서버로 전송되야 하므로 해킹의 위험이 있음.
* 따라서 모바일 지갑 내부에 **private key 로 transaction 을 sign** 하는 기능이 있어야함.
* 해당 모바일 지갑이 자체적으로 sign 기능을 갖추고 있는지 알아보려면 `nodeos`만 돌아가고 있는 서버로 host 를 변경하여 정상적으로 transaction 이 이뤄지는지를 확인하면 됨.(토큰전송, Ram 구입/판매, cpu/network 할당/반환, 투표 등)




