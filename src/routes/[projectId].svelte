<a href="https://ncodes.eu"><img src="https://d6scj24zvfbbo.cloudfront.net/e3cd589ac11969a06b1927cf04fd305f/200000045-0d7880d78a/700/logo_512x512.png" alt="nCodes" width="5%" height="5%"></a>

<div class=" bg-[#4747477e] filter drop-shadow-md md:drop-shadow-xl rounded-3xl p-10 mt-16 mr-32 ml-32">
    <div class="flex flex-col my-auto items-center">

        <p class="text-center text-5xl text-[#7900ff] filter drop-shadow-md md:drop-shadow-xl font-bold">{topic}</p> <br>
        <div class="bg-[#7900ff] filter drop-shadow-md md:drop-shadow-xl rounded-3xl p-1 mt-1 mr-1 ml-1 w-32"></div>

    </div>
    <p class=" text-[#f0f0f0] mt-12">{@html readme}</p>
</div>

<div class=" bg-[#4747477e] filter drop-shadow-md md:drop-shadow-xl rounded-3xl p-10 mt-16 mr-32 ml-32">
    <div class="flex flex-col my-auto items-center">

        <p class="text-center text-5xl text-[#7900ff] filter drop-shadow-md md:drop-shadow-xl font-bold">Gallery</p> <br>
        <div class="bg-[#7900ff] filter drop-shadow-md md:drop-shadow-xl rounded-3xl p-1 mt-1 mr-1 ml-1 w-32"></div>

    </div>
    <p class=" text-[#f0f0f0] mt-12">insert</p>
</div>

<div class=" bg-[#4747477e] filter drop-shadow-md md:drop-shadow-xl rounded-3xl p-10 mt-16 mr-32 ml-32">
    <div class="flex flex-col my-auto items-center">

        <p class="text-center text-5xl text-[#7900ff] filter drop-shadow-md md:drop-shadow-xl font-bold">Links</p> <br>
        <div class="bg-[#7900ff] filter drop-shadow-md md:drop-shadow-xl rounded-3xl p-1 mt-1 mr-1 ml-1 w-32"></div>

    </div>
    <p class=" text-[#f0f0f0] mt-12">insert</p>
</div>

<script>

    import {page} from '$app/stores';
    import showdown from 'showdown';

    let topic = "topic";
    let readme = "readme";
    const url = "https://raw.githubusercontent.com/nCodesDotEU";
    const projectId = $page.path;

    async function readWriteAsync() {

        await fetch(url + projectId + "/master/README.md")
        .then(response => response.text())
        .then(result => {
            const converter = new showdown.Converter({metadata: true});
            converter.setOption('tables', true);
            converter.setOption('tasklists', true);
            converter.setOption('noHeaderId', true);
            converter.setFlavor('github');
            let body = converter.makeHtml(result);
            body = setStyle(body);
            readme = body;
            topic = projectId.substr(1);
            topic = topic.split('-').join(' ');
        });

    }
    readWriteAsync();

    function setStyle(html){
        html = html.split('<h1>').join('<h1 class=" text-[#7900ff] text-3xl filter drop-shadow-md md:drop-shadow-xl font-bold">');
        html = html.split('<h2>').join('<h2 class=" mt-4 text-[#7900ff] text-2xl filter drop-shadow-md md:drop-shadow-xl font-bold">');
        html = html.split('<h3>').join('<h3 class=" mt-2 text-[#7900ff] text-xl filter drop-shadow-md md:drop-shadow-xl font-bold">');
        html = html.split('<ol>').join('<ol class=" list-disc ml-4"">');
        html = html.split('<ul>').join('<ul class=" list-disc ml-4"">');
        html = html.split('<code>').join('<code class=" bg-[#453e4b] rounded-md">');
        html = html.split('<pre>').join('<pre class=" bg-[#453e4b] rounded-md w-1/2">');
        html = html.split('<table>').join('<table class=" bg-[#505050] w-1/2 shadow-md rounded">')
        html = html.split('<thead>').join('<thead class=" bg-[#3b3b3b]">');
        html = html.split('<th>').join('<th class=" px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider  p-4>');
        html = html.split('<td>').join('<td class=" text-center">');
        html = html.split('<p>').join('<p class=" ml-4">');
        html = html.split('<a href="').join('<a class=" text-[#a48dbe] underline" href="');
        return html;
    }


</script>

<h1 class=" list-disc"></h1>