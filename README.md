---


---

<h1 id="commmune">Commmune</h1>
<ul>
<li><a href="#the-community-management-app">Description and goals</a></li>
<li><a href="#learning-process">Learning process</a></li>
<li><a href="https://github.com/CamilleBC/Commune#">https://github.com/CamilleBC/Commune#</a>
<ul>
<li><a href="#20180920-commit-938fcfa">2018/09/20</a>: <em>ContentProvider</em> with <em>CursorLoader</em>, a <em>RecyclerView</em> and a custom adapter.</li>
<li><a href="#20180921-commit-9f579e6">2018/09/21</a>: <em>SearchView</em>, custom query for the <em>CursorLoader</em>, and photo thumbnail’s URI.</li>
<li><a href="#to-be-continued...">To be continued…</a></li>
</ul>
</li>
</ul>
<h2 id="the-community-management-app">The community management app</h2>
<p>My first goal with Commune is to understand how to articulate the different Android components, the <a href="https://matrix.org/">Matrix</a> protocol, and manage event planning as well. We’ll see where it goes from there.</p>
<p>The ultimate goal is the far future is to create an open-source tool to manage communities of various size. Just one app to communicate with your friends, coworkers, co-citizens, etc.<br>
Send a simple message, create a group chat, plan an event and share some interesting stuff.</p>
<h2 id="learning-process">Learning process</h2>
<p>I will try to describe in a chronological order what my project taught me about Android apps’ architecture and development.</p>
<h3 id="commit-938fcfa">[2018/09/20] <a href="https://github.com/CamilleBC/Commune/commit/938fcfa4d478ac0a3d59ddcf3d1a5f2567e31e59">commit 938fcfa</a></h3>
<p>At this stage, I am discovering the way Android manages data.<br>
The <a href="https://developer.android.com/training/contacts-provider/retrieve-names">android guide</a> describes a way to link a <em>SimpleCursorLoarder</em> to a <em>ListView</em>.<br>
I have tried to use a <em>RecyclerView</em> adapter because it is much more versatile than the basic <em>ListView</em>. The <em>RecyclerView</em> doesn’t have an easy way to plug the <em>CursorLoader</em> in. I have used an <a href="https://forums.bignerdranch.com/t/using-a-recyclerview-with-a-loader-cursorloader/8286/3">implementation</a>  found on the web, that I have tried to understand and implement. I have not yet cleaned it, nor did I try to use “proper” Kotlin syntax.<br>
I first tried to replace the <em>CursorLoader</em> by a <em>ViewModel</em> with a <em>Room</em> and some <em>DAO</em> (Data Access Object) and <em>LiveData</em>, before understanding that both were an API layer on some Database. I had to either create a custom <em>Room</em>+<em>ViewModel</em> layer to get data from the phone’s contact database, or reuse the existing <em>ContentProvider</em> with a <em>CursorLoader</em>. I chose to do the latter, as I don’t feel confident enough yet to create my own custom layer.</p>
<p><strong>As of now</strong> the app only displays a list of all contacts in the phone. It updates in real time when the contacts are updated on the phone.</p>
<h3 id="commit-9f579e6">[2018/09/21] <a href="https://github.com/CamilleBC/Commune/commit/9f579e68a6b1731a99e8c3fda35960e148fe1579">commit 9f579e6</a></h3>
<p>I implemented a menu with a <em>SearchView</em>. On text edition and submission, the SQL query is upated, sent to the <em>CursorLoader</em>, and the <em>LoaderManager</em> is restarted. It doesn’t wait for completion when the user is typing, as there is no need to wait for the <em>CursorLoader</em> to return if the query is updating.<br>
I also request the thumbnail URI to display a picture on the <em>RecyclerView</em>, as I find it nicer to look at.</p>
<h3 id="to-be-continued...">To be continued…</h3>
<p>I have started to implement the searchable interface to the activity. The plan is for the activity to be callable with an <em>Intent</em>, and to be able to return a contact’s data, either on user selection or because only one result fits, or a failure if no contact matches the query.</p>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

