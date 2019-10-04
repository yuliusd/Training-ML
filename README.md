
 <div id="readme" class="Box-body readme blob instapaper_body js-code-block-container">
    <article class="markdown-body entry-content p-3 p-md-6" itemprop="text"><h2><a id="user-content-overview" class="anchor" aria-hidden="true" href="#overview"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Overview</h2>
<p>The <code>xgboost-training-cm.py</code> pipeline creates XGBoost models on structured data in CSV format. Both classification and regression are supported.</p>
<p>The pipeline starts by creating an Google DataProc cluster, and then running analysis, transformation, distributed training and
prediction in the created cluster. Then a single node confusion-matrix aggregator is used (for classification case) to
provide the confusion matrix data to the front end. Finally, a delete cluster operation runs to destroy the cluster it creates
in the beginning. The delete cluster operation is used as an exit handler, meaning it will run regardless of whether the pipeline fails
or not.</p>
<h2><a id="user-content-requirements" class="anchor" aria-hidden="true" href="#requirements"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Requirements</h2>
<p>Preprocessing uses Google Cloud DataProc. Therefore, you must enable the <a href="https://cloud.google.com/endpoints/docs/openapi/enable-api" rel="nofollow">DataProc API</a> for the given GCP project.</p>
<h2><a id="user-content-compile" class="anchor" aria-hidden="true" href="#compile"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Compile</h2>
<p>Follow the guide to <a href="https://www.kubeflow.org/docs/guides/pipelines/build-pipeline/" rel="nofollow">building a pipeline</a> to install the Kubeflow Pipelines SDK and compile the sample Python into a workflow specification. The specification takes the form of a YAML file compressed into a <code>.zip</code> file.</p>
<h2><a id="user-content-deploy" class="anchor" aria-hidden="true" href="#deploy"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Deploy</h2>
<p>Open the Kubeflow pipelines UI. Create a new pipeline, and then upload the compiled specification (<code>.zip</code> file) as a new pipeline template.</p>
<h2><a id="user-content-run" class="anchor" aria-hidden="true" href="#run"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Run</h2>
<p>Most arguments come with default values. Only <code>output</code> and <code>project</code> need to be filled always.</p>
<ul>
<li><code>output</code> is a Google Storage path which holds
pipeline run results. Note that each pipeline run will create a unique directory under <code>output</code> so it will not override previous results.</li>
<li><code>project</code> is a GCP project.</li>
</ul>
<h2><a id="user-content-components-source" class="anchor" aria-hidden="true" href="#components-source"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Components source</h2>
<p>Create Cluster:
<a href="https://github.com/kubeflow/pipelines/tree/master/components/deprecated/dataproc/create_cluster/src">source code</a>
<a href="https://github.com/kubeflow/pipelines/tree/master/components/deprecated/dataproc/create_cluster">container</a></p>
<p>Analyze (step one for preprocessing):
<a href="https://github.com/kubeflow/pipelines/tree/master/components/deprecated/dataproc/analyze/src">source code</a>
<a href="https://github.com/kubeflow/pipelines/tree/master/components/deprecated/dataproc/analyze">container</a></p>
<p>Transform (step two for preprocessing):
<a href="https://github.com/kubeflow/pipelines/tree/master/components/deprecated/dataproc/transform/src">source code</a>
<a href="https://github.com/kubeflow/pipelines/tree/master/components/deprecated/dataproc/transform">container</a></p>
<p>Distributed Training:
<a href="https://github.com/kubeflow/pipelines/tree/master/components/deprecated/dataproc/train/src">source code</a>
<a href="https://github.com/kubeflow/pipelines/tree/master/components/deprecated/dataproc/train">container</a></p>
<p>Distributed Predictions:
<a href="https://github.com/kubeflow/pipelines/tree/master/components/deprecated/dataproc/predict/src">source code</a>
<a href="https://github.com/kubeflow/pipelines/tree/master/components/deprecated/dataproc/predict">container</a></p>
<p>Confusion Matrix:
<a href="https://github.com/kubeflow/pipelines/tree/master/components/local/confusion_matrix/src">source code</a>
<a href="https://github.com/kubeflow/pipelines/tree/master/components/local/confusion_matrix">container</a></p>
<p>ROC:
<a href="https://github.com/kubeflow/pipelines/tree/master/components/local/roc/src">source code</a>
<a href="https://github.com/kubeflow/pipelines/tree/master/components/local/roc">container</a></p>
<p>Delete Cluster:
<a href="https://github.com/kubeflow/pipelines/tree/master/components/deprecated/dataproc/delete_cluster/src">source code</a>
<a href="https://github.com/kubeflow/pipelines/tree/master/components/deprecated/dataproc/delete_cluster">container</a></p>
</article>
  </div>

    </div>
