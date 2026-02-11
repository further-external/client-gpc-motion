# client-gpc-motion
<h1 id="overview"><strong>Overview</strong></h1>
<p>This repository contains the necessary specifications to build an event driven data layer.</p>
<h2 id="adobe-launch-deployment">Adobe Launch Deployment</h2>
<p>The embed code is a <strong>script</strong> tag that you put on your web pages to load and execute the logic you build in Launch. If you load the library asynchronously, the browser continues to load the page, retrieves the Launch library, and executes it in parallel. In this case, there is only one embed code, which you put in the <code>&lt;head&gt;</code> (When Launch is deployed synchronously, there are two embed codes, one which you put in the <code>&lt;head&gt;</code> and another which you put before the <code>&lt;/body&gt;</code>).</p>
<p>From the property Overview screen, click on the Environments tab to go to the environments page (Note that Development, Staging, and Production environments have been pre-created for you):</p>
<div data-node-type="mediaSingle" data-layout="center" class="rich-media-item mediaSingleView-content-wrap image-center sc-ePZHVD kLKZTy sc-bEjcJn jjvZSm"><div class="sc-bGbJRg kUjBNf"><div data-testid="media-card-view" class="new-file-experience-wrapper sc-eeMjtc czMCpw"><div data-test-status="complete" data-test-media-name="https://apollo-help-images.s3.amazonaws.com/launch_embed_1.png" data-testid="media-file-card-view" class="media-file-card-view sc-bhizqx jGLuht"><img data-testid="media-image" height="345" width="746" alt="" src="https://apollo-help-images.s3.amazonaws.com/launch_embed_1.png" draggable="false" class="sc-drKuOJ eHwasM"></div></div></div></div>
<p>Development, Staging, and Production environments correspond to the typical environments in the code development and release process. Code is first written by a developer in a Development environment. When they have completed their work, they send it to a Staging environment for QA and other teams to review. Once the QA and other teams are satisfied, the code is then published to the Production environment, which is the public-facing environment which your visitors experience when they come to your website.</p>
<p>Launch permits additional Development environments, which is useful in large organizations in which multiple developers are working on different projects at the same time.</p>
<p>These are the only environments we need to complete the tutorial. Environments allow you to have different working versions of your Launch libraries hosted at different URLs, so you can safely add new features and make them available to the right users (e.g. developers, QA engineers, the public, etc.) at the right time.</p>
<p>Now, let's copy the embed code:</p>
<ol>
<li><p>In the Development row, click the Install icon to open the modal. Note that Launch will default to the asynchronous embed codes.</p></li>
<li><p>Click the Copy icon to copy the embed code to your clipboard.</p></li>
<li><p>Click Close to close the modal.</p></li>
</ol>


<div data-node-type="mediaSingle" data-layout="center" class="rich-media-item mediaSingleView-content-wrap image-center sc-ePZHVD kLKZTy sc-bEjcJn jjvZSm"><div class="sc-bGbJRg jSORbV"><div data-testid="media-card-view" class="new-file-experience-wrapper sc-eeMjtc TbWkh"><div data-test-status="complete" data-test-media-name="https://apollo-help-images.s3.amazonaws.com/launch_embed_2.png" data-testid="media-file-card-view" class="media-file-card-view sc-bhizqx jGLuht"><img data-testid="media-image" height="430" width="743" alt="" src="https://apollo-help-images.s3.amazonaws.com/launch_embed_2.png" draggable="false" class="sc-drKuOJ eHwasM"></div></div></div></div>
<h3 id="implement-the-embed-code-in-the-of-the-sample-html-page">Implement the Embed Code in the of the Sample HTML Page</h3>
<p>The embed code should be implemented in the element of all HTML pages that will share the property. You might have one or several template files which control the globally across the site, making it a straightforward process to add Launch.</p>
<div class="code-block sc-cMjzQU dEWtyV"><span data-ds--code--code-block="" data-code-lang="" class="prismjs css-1xfvm4v"><code><span class="comment linenumber react-syntax-highlighter-line-number">1</span><span class="">&lt;!--Launch Header Embed Code: REPLACE LINE 39 WITH THE EMBED CODE FROM YOUR OWN DEVELOPMENT ENVIRONMENT--&gt; </span><span class="comment linenumber react-syntax-highlighter-line-number">2</span>&lt;script src="&lt;your_library_url&gt;" async&gt;&lt;/script&gt; <span class="comment linenumber react-syntax-highlighter-line-number">3</span>&lt;!--/Launch Header Embed Code--&gt; </code></span></div>
<p>Make sure you build a version of the library and then test that the JS file is correctly loading on the page.</p>
<p>For more information refer to the&nbsp;<a title="https://docs.adobe.com/content/help/en/core-services-learn/implementing-in-websites-with-launch/configure-launch/launch.html" href="https://docs.adobe.com/content/help/en/core-services-learn/implementing-in-websites-with-launch/configure-launch/launch.html">official documentation</a>.</p>
<h2 id="data-layer">Data Layer</h2>
<p>Each file inside the events folder corresponds to a single use case or site event that needs to be implemented. These events are leveraged to trigger tracking rules in the tag management tool of choice and share data with the analytics reporting tool.</p>
<p>As the data layer is event-based, the order in which the events are fired is critical. In general, events should be pushed onto the data layer in the following sequence when a page load (virtual or otherwise) occurs:</p>
<p>Page Load Started &gt; <em>Other Page-level Events</em> &gt; Page Load Completed</p>
<p>If an Event is part of the page load sequence, it will be indicated in the corresponding event file.</p>
<p>Events that occur outside of the page load sequence should be pushed onto the data layer as they occur.</p>
<h2 id="questionscomments">Questions/Comments</h2>
<p>For any questions or comments, please contact&nbsp;brad.davis@gofurther.com.</p>
