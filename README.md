## Uso
Incluir JS

    code.jquery.com/jquery-1.11.2.min.js


## Função para carregar playlist Youtube

    $(document).ready(function(){
        var objectUrlInicial;
        var objectTituloInicial;
        var paginaAtual = 1;
        var maximoResultado = 7;

    $('#carregarMaisVideos').click(function(e) {
        e.preventDefault();
        carregarVideos();
    });

    //Carregar Vídeo Youtube

    carregarVideos();
    function carregarVideos(){
        $.getJSON('http://gdata.youtube.com/feeds/api/videos?alt=json-in-script&orderby=published&&start-index='+paginaAtual+'&max-results='+maximoResultado+'&author={ID-DO-USUÁRIO-YOUTUBE}&callback=?',     function(data){

    if('entry' in data.feed){
        $.each(data.feed.entry, function(i,item){
            var principal = $('< li>< /li>');
            var linkVideo = $('');
            var thumb = $('< img src="'+item.media$group.media$thumbnail[1].url+'" alt="Assistir ao vídeo" />');

    if(i == 0){
        objectTituloInicial = item.title.$t;
            objectUrlInicial = item.media$group.media$content[0].url;
    }

    $(linkVideo).attr('href', 'videos?video='+item.media$group.media$content[0].url); tempo_video =     Math.round(item.media$group.yt$duration.seconds/60);

    $(linkVideo).append(thumb);
    $(linkVideo).append(item.title.$t);
    $(principal).append(linkVideo);
    $('#listaVideos').append(principal);
    $('#listaVideos .btn_carregar_mais').appendTo('#listaVideos');

        principal).find('a').click(function(event){
            event.preventDefault();
            $('#videoPrincipalPlayer').attr('src', item.media$group.media$content[0].url);
            $('#videoPrincipal #tituloVideo').text(item.title.$t);
            $('#videoPrincipal #tituloVideo').hide();
            $('#videoPrincipal #tituloVideo').slideDown();
            $(document).scrollTop(135);
        });

    });
    } else {
        $('.btn_carregar_mais').hide();
    }
    if(paginaAtual == 1){
        $('#videoPrincipalPlayer').attr('src', objectUrlInicial);
        $('#videoPrincipal #tituloVideo').text(objectTituloInicial);
    }
        paginaAtual += 7; maximoResultado = 6; });
    }

    });


## Vídeo principal
    <div id="videoPrincipal">
        <iframe id="videoPrincipalPlayer" src="" frameborder="0" allowfullscreen></iframe>
    </div>

## Titulo principal
    <div id="tituloVideo"></div>

## Listagem de vídeos da playlist

    <ul id="listaVideos">
        <li class="btn_carregar_mais">
            <a id="carregarMaisVideos" href="#">
                Carregar <img src="static/img/videos/mais.png" alt="mais" />
            </a>
        </li>
    </ul>


