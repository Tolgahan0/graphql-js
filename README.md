# GraphQL.js

Facebook tarafından oluşturulan API'ler için bir sorgu dili olan GraphQL için JavaScript referans uygulamasıdır.

[![npm version](https://badge.fury.io/js/graphql.svg)](https://badge.fury.io/js/graphql)
[![Build Status](https://github.com/graphql/graphql-js/workflows/CI/badge.svg?branch=main)](https://github.com/graphql/graphql-js/actions?query=branch%3Amain)

Daha eksiksiz belgelere şu adresten bakın: https://graphql.org / ve
https://graphql.org/graphql-js /.

Yardım mı arıyorsunuz? Kaynakları bulun [topluluktan](https://graphql.org/community /).

## Başlabgıç

Graphql'e genel bir bakış aşağıda ki linkte mevcuttur:
[BENİOKU](https://github.com/graphql/graphql-spec/blob/main/README.md ) için
[GraphQL için şartname] (https://github.com/graphql/graphql-spec ). Genel bakış
[tests](src/__tests__) olarak var olan basit bir GraphQL örnekleri kümesini açıklar.

### GraphQl.js Kullanmak

GraphQL.js'i aşağıda ki npm'i kullanarak indirin

Npm linki

```sh
npm install --save graphql
```

 veya yarn kullanabilirsin :

```sh
yarn add graphql
```

GraphQL.js iki önemli yetenek sağlar: bir tür şeması oluşturmak ve
bu tür şemaya karşı sorgular sunmak.

İlk olarak, kod tabanınızla eşleşen bir GraphQL tipi şema oluşturun.

```js
import {
  graphql,
  GraphQLSchema,
  GraphQLObjectType,
  GraphQLString,
} from 'graphql';

var schema = new GraphQLSchema({
  query: new GraphQLObjectType({
    name: 'RootQueryType',
    fields: {
      hello: {
        type: GraphQLString,
        resolve() {
          return 'world';
        },
      },
    },
  }),
});
```

Bu, çözümleyen bir tür ve bir alan içeren basit bir şema tanımlar
sabit bir değere. 'Çözümle' işlevi bir değer, bir söz döndürebilir,
ya da bir dizi söz. Daha karmaşık bir örnek, üst düzey [testler](src /__testler__) dizinine dahil edilmiştir.

Ardından, bu tür şemaya karşı bir sorgunun sonucunu sunun.

```js
var source = '{ hello }';

graphql({ schema, source }).then((result) => {
  // Prints
  // {
  //   data: { hello: "world" }
  // }
  console.log(result);
});
```
Bu, tanımlanan bir alanı getiren bir sorgu çalıştırır. `Graphql' işlevi
önce yürütmeden önce sorgunun sözdizimsel ve anlamsal olarak geçerli olduğundan emin olun
aksi takdirde hataları bildirir.

```js
var source = '{ BoyHowdy }';

graphql({ schema, source }).then((result) => {
  // Prints
  // {
  //   errors: [
  //     { message: 'Cannot query field BoyHowdy on RootQueryType',
  //       locations: [ { line: 1, column: 3 } ] }
  //   ]
  // }
  console.log(result);
});
```

** Not **: Bir üretim sunucusu çalıştırıyorsanız lütfen `NODE_ENV =production' ayarlamayı unutmayın. Geliştirme sırasında yararlı olabilecek ancak performansı önemli ölçüde artıracak bazı kontrolleri devre dışı bırakacaktır.

### En güncel teknoloji ile çalışmak ister misin ?

Bu depodaki `npm'nin şubesi otomatik olarak son şube olarak korunur
npm'de bulunan aynı biçimde tüm testleri geçmek için 'ana' taahhüt edin. O
birçok nedenden dolayı npm'e dağıtılan yapıları kullanmanız önerilir, ancak kullanmak istiyorsanız
graphql-js'nin henüz yayınlanmamış en son sürümü, bunu aşağıdakilere bağlı olarak yapabilirsiniz
Aşağıdakini indirin:
```
npm install graphql@git://github.com/graphql/graphql-js.git#npm
```

### Tarayıcıda kullanmak ?

GraphQL.js genel amaçlı bir kütüphanedir ve her ikisi de bir bağıl sunucusunda ve tarayıcıda kullanılabilir
 Örnek olarak, [GraphiQL](https://github.com/graphql/graphql /)
araç GraphQL.js ile oluşturulmuştur.

GraphQL.js kullanarak bir proje oluşturmak [webpack] ile  (https://webpack.js.org ) veya
[[roll up](https://github.com/rollup/rollup ) çalışmalı ve sadece şunları içermelidir
kullandığınız kütüphanenin bölümleri. Bu işe yarıyor çünkü GraphQL.js dağıtıldı
hem CommonJS (`require ()`) hem de Module (`import') dosyaları . Herhangi bir
özel yapı yapılandırmaları arayın ( `.mj' dosyaları)

### Katkı

Destek taleplerini aktif olarak memnuniyetle karşılıyoruz. Nasıl katkıda bulunacağınızı öğrenin (./.github/CONTRİBUTİNG.md).

Bu depo Easy CIA tarafından yönetilmektedir. Proje katılımcıları katkıda bulunmadan önce ücretsiz ([GraphQL Spesifikasyonu Üyelik sözleşmesi]) imzalamalıdır. (https://preview-spec-membership.graphql.org )  Bunu yalnızca bir kez yapmanız gerekir ve [bireysel katkıda bulunanlar] tarafından imzalanabilir (http://individual-spec-membership.graphql.org /) veya [işverenleri] (http://corporate-spec-membership.graphql.org /).

İmza sürecini başlatmak için lütfen bu repoya karşı bir PR açın. Sizden hala bir üyelik anlaşması talebimiz  olursa Easy sınıfı birleşmeyi engelleyecektir.

[Detaylı bilgiyi burada bulabilirsiniz](https://github.com/graphql/graphql-wg/tree/main/membership ). Sorunlarınız varsa, lütfen e-posta gönderin [operations@graphql.org ](mailto:operations@graphql.org ).

Şirketiniz graphql'den yararlanıyorsa ve topluluğumuza güç veren sistemler ve kişiler için gerekli finansal desteği sağlamak istiyorsanız, lütfen [GraphQL Vakfı'na] üyeliği de göz önünde bulundurun (https://foundation.graphql.org/join ).

### Değişiklik takipleme

Değişiklikler [GitHub sürümleri] olarak izlenir (https://github.com/graphql/graphql-js/releases ).

### Lisans

GraphQL.js [MIT lisanslıdır](./LİSANS).
