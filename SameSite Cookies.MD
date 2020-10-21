#SameSite Cookies

#### Cookies
Cookies são um dos métodos disponíveispara adicionar estado persistente a sites. Os navagadores estão mudando seu comportamento para impor mais padrões de preservação de privacidade.

 * key = value
    * session = a451ds1d54s66kj
 * Set-Cookie, forma que o servidor definem cookies
 * document.cookie (js), forma com que o navegador adiciona ou lê os cookies.
 
Normalmente os cookies são enviados a cada solicitação havendo sobrecarga e adicionando um atraso no seu tempo para o primeiro byte. Seja conservador no número e no tamanho dos coookies e use *Max-Age* para garantir expiração.

#### Cookies primários e de tercerios
  * Primários são aqueles que correspondem ao domínio atual, ou seja, contexto atual.
  * Terceiros são aqueles que correspondem a domínios diferentes do atual.
  
#### Problemas
  * Cookies de terceiros podem manter o estado
      * Cookies não útil para o seu site atual
          * por ex: quando usamos um link de imagem de um outra site para exibir no nosso site atual. Este link pode enviar um cookies por meio da solicitação da imagem adicionando sobrecarga à solicitação.
      * Cookies utéis
          * por ex: se incorporar um vídeo do youtube no seu site há a opção de "Assistir mais tarde" no player, por meio de um cookie de terceiro no caso, ele salvará automáticamente este vídeo a sua playlist sem precisar acessar a página direta do YouTube.
  * Ataques de falsificação de solicitação entre sites (CSRF) baseiam-se no fato de que os cookies são anexados a qualquer dolicitação para uma determinada origem, não importa quem inicia a solicitação.
  
#### SameSite
Esta atributo permite declarar se o cookie deve ser restrito a um contexto primário ou do mesmo site.

  * Same-site - www.web.dev solicita uma imagem em static.web.dev.
  * Cross-site - your-project.github.io solicita uma imagem em my-project.github.io
  
  [Saiba mais](https://web.dev/same-site-same-origin/)
  
O atributo SameSite possui 3 atributos:
  * Strict - cookie enviado apenas para o contexto original.
      * ex: alterar senha ou fazer uma compra, ou seja, ações que o seu usuário esta realizando.
  * Lax - permite que o cookie seja enviado com navegações de nível superior, ou seja, diretas para a página. 
      * ex: cookies que afetam a exibição do site.
  * None - cookie é enviado para todos os contextos
      * ex: pode ser usado para comunicar claramente que deseja que o cookie seja enviado em um contexto de terceiros.
  
> Atenção: Nem Strict nem Lax são uma solução completa para a segurança do seu site. Os cookies são enviados como parte da solicitação do usuário e você deve tratá-los da mesma forma que qualquer outra entrada do usuário. Isso significa higienizar e validar a entrada. Nunca use um cookie para armazenar dados que você considera um segredo do lado do servidor.

Por padrão
  * Cookies sem SameSite são tratados como SameSite=Lax.
  * Cookies com SameSite = None também devem especificar Secure, o que significa que requerem um contexto seguro.
      * ex: Set-Cookie: promo_shown=1; Max-Age=2600000; SameSite = None; Secure

Caso o seu chrome não esteja na versão atual, podemos utilizar esta flag para testar este comportamento.
> Você pode testar esse comportamento a partir do Chrome 76 ativando chrome://flags/#cookies-without-same-site-must-be-securee do Firefox 69 about:configconfigurando network.cookie.sameSite.noneRequiresSecure.



fonte: [web.dev, Rowan Merewood, Explicação](https://web.dev/samesite-cookies-explained/?utm_source=devtools)
fonte: [web.dev, Eiji Kitamura, Same-origins x Cross-origins](https://web.dev/same-site-same-origin/)
