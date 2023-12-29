# Go语言SM2,SM3,SM4实现
- 支持JAVA, C1C3C2， C1C2C3 排序算法。
- 支持招行JAVA Sm2SignWithSm3实现
- 国密SM2算法实现，支持国密SM2签名，国密SM2加密，国密SM2验签，
- 国密SM2密钥交换，国密SM2密钥生成，国密SM2密钥转换，
- 国密SM2密钥导入导出，国密SM2密钥对生成


#### 使用方法

* 签名:
```go

import (
	"encoding/base64"
	"encoding/hex"
	"errors"
    "byte"
    "github.com/dcto/smn"
)

func Sign(data []byte) ([]byte, error) {
	privateKeyByte, err := hex.DecodeString("私钥HEX")
	if err != nil {
		logx.Error(err)
		return nil, err
	}
	
	privateKey, err := sm2.RawBytesToPrivateKey(privateKeyByte)
	if err != nil {
		logx.Error(err)
		return nil, err
	}
	//国密局SM2密码
	signBytes, err := sm2.Sign(privateKey, []byte("1234567812345678"), []byte(data))

	if err != nil {
		logx.Error(err)
		return nil, err
	}
	return signBytes, nil

}

```

加密：
```go
import (
	"encoding/base64"
	"encoding/hex"
	"errors"
    "byte"
    "github.com/dcto/smn"
)

func Encrypt(data []byte) ([]byte, error) {

	pubkeyBytes, err := hex.DecodeString("公钥HEX")
	if err != nil {
		logx.Error(err)
		return nil, err
	}
	pubkey, err := sm2.RawBytesToPublicKey(pubkeyBytes)

	if err != nil {
		logx.Error(err)
		return nil, err
	}

	ciphertxt, err := sm2.Encrypt(pubkey, data, 2)

	if err != nil {
		logx.Error(err)
		return nil,err
	}
	return ciphertxt, nil
}

```

解密：
```go
import (
	"encoding/base64"
	"encoding/hex"
	"errors"
    "byte"
    "github.com/dcto/smn"
)

func Decrypt(data []byte) ([]byte, error) {

	privateKeyByte, err := hex.DecodeString(s.Config.Cert.PriKey)
	if err != nil {
		logx.Error(err)
		return nil, err
	}
	
	privateKey, err := sm2.RawBytesToPrivateKey(privateKeyByte)

	if err != nil {
		logx.Error(err)
		return nil, err
	}
	dataPlain , err := sm2.Decrypt(privateKey, data, 2)
	if err != nil {
		logx.Error(err)
		return nil, err
	}

	logx.Debug(string(dataPlain))
	return nil, nil
}
```



#### 声明
本库Fork自原作者的声明:

梧桐链: [gjfoc](github.com/tjfoc/gmsm/sm2)

ZZMarquis: [ZZMarquis](github.com/dcto/smx/sm2)

ZZMarquis版本修改，增加部份说明及招行Java接口 HEX密钥对实现。