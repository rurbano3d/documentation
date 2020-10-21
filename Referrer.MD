# Melhores práticas com Referrer

* Vazamento inesperado de informações de cross-origin prejudica a privacidade dos usuário. Uma política de referência de proteção pode ajudar.
* O ideial é utilizar uma política de referência *strict-origin-when-cross-origin*, retendo muito da utilidade do referenciador, ao mesmo tempo reduz o risco de vazamento de cross-origins de dados.
* Não use referenciadores para proteção Cross-site Request Forgery (CSRF). Em vez disso, use Tokens CSRF e outros cabeçalhos como uma camada extra de segurança.

> O Referer cabeçalho está sem um R, devido a um erro de ortografia original na especificação. O Referrer-Policy cabeçalho e referrer em JavaScript e o DOM estão escritos corretamente.

#### Referrer-Policy 101
As solicitações HTTP podem incluir o *Referer* opcional que indica a origem ou a URL da página. A Referrer-Policy define quais dados são disponibilizados no *Referer Header*.

Algumas solicitações podem enviar dados que deveriam estar mais seguros através de um url completa pelo *Referer Header*, para restringir quais dados de referenciar são disponibilizados você pode definir uma política de referenciador.

Dados disponíveis no *Referer Header*.
  * No data - Sem dados(nenhum *Referer Header* esta presente;
  * Origin Only - Apenas a origem
  * Full URL - O URL completo: origem , caminho e string de consulta
  
Existem 8 políticas, vamos separa-las por categorias:
  * Políticas que não consideram o contexto da solicitação.
      * no-referrer, sem dados.
      * origin, apenas a origem 
      * unsafe_url, URL completa com origem, caminho e string de consulta.
  * Políticas que se concentram em saber se a solicitação é feita para um destino menos seguro do que de onde a solicitação veio. Isso ajuda a atingir as metas de segurança.
      * strict-origin
        * HTTPS para HTTP, sem dados.
        * HTTPS para HTTPS ou HTTP para HTTP, apenas a origem.
      * no-referrer-when-downgrade
        * HTTPS para HTTP, sem dados.
        * HTTPS para HTTPS ou HTTP para HTTP, URL completa com origem, caminho e string de consulta.
  * Políticas focadas em se a solicitação é cross-origins ou same-origins. Isso ajuda a alcançar objetivos de privacidade
      * origins-when-cross-origins
        * cross-origins request, apenas origen.
        * same-origin request, URL completa com origem, caminho e string de consulta.
      * same-origin
        * cross-origin request, sem dados.
        * same-origin request, URL completa com origem, caminho e string de consulta.
  * Políticas voltadas para a segurança da solicitação e se ela é cross-origin ou same-origin, ajuda a atingir os objetivos de privacidade e segurança.
      * strict-origin-when-cross-origin
        * HTTPS para HTTP, sem dados.
        * cross-origin request, HTTPS to HTTPS ou HTTP TO HTTP, apenas origem.
        * same-origin request, URL completa com origem, caminho e string de consulta.
        
> Quando ocorre solicitações HTTPS para HTTP ocorre downgrade de segurança, ou seja, se a solicitação pode expor dados de uma origem criptografada para uma não criptografada. Se forem da mesma origem , isso significa que o esquema (HTTPS ou HTTP) é o mesmo, portanto, não há downgrade de segurança.

A partir de Julho de 2020 se nenhuma política for definida os navegadores terão uma política padrão.
  * Chrome, Safari
    * strict-origin-when-cross-origin
  * Firefox, Edge
    * no-referrer-when-downgrade
    * strict-origin-when-cross-origin
    

fonte: [web.dev, Maud Nalpas, Melhores práticas](https://web.dev/referrer-best-practices/)
fonte: [web.dev, Eiji Kitamura, Same-origins x Cross-origins](https://web.dev/same-site-same-origin/)
