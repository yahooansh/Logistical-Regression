# Logistical-Regression
create a Logistical Regression model and associated 
ROC/AUC curve for his raisin_dataset.csv dataset in order to predict raisin type.
The dataset has 900 observations and 8 variables:
Independent Variables
Area: Gives the number of pixels within the boundaries of the raisin. 
Perimeter: It measures the environment by calculating the distance between the boundaries of the raisin 
and the pixels around it. 
MajorAxisLength: Gives the length of the main axis, which is the longest line that can be drawn on the 
raisin. 
MinorAxisLength: Gives the length of the small axis, which is the shortest line that can be drawn on 
the raisin. 
Eccentricity: It gives a measure of the eccentricity of the ellipse, which has the same moments as 
raisins. 
ConvexArea: Gives the number of pixels of the smallest convex shell of the region formed by the 
raisin. 
Extent: Gives the ratio of the region formed by the raisin to the total pixels in the bounding box. 

Dependent Variable
Class: Kecimen and Besni raisin.
![Screenshot 2024-10-26 131746](https://github.com/user-attachments/assets/fc288760-3223-43bc-986f-14d89a45ac9c)
[Presentation.pptx](https://github.com/user-attachments/files/17531434/Presentation.pptx)

[Uploadin<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd"><html><head></head><body>















    




    
    
    
    

<div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&#160;[1]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor">
     <div class="CodeMirror cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="kn">import</span> <span class="nn">numpy</span> <span class="k">as</span> <span class="nn">np</span>
<span class="kn">import</span> <span class="nn">pandas</span> <span class="k">as</span> <span class="nn">pd</span>
<span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="k">as</span> <span class="nn">plt</span>
<span class="o">%</span><span class="k">matplotlib</span> inline
<span class="kn">import</span> <span class="nn">seaborn</span> <span class="k">as</span> <span class="nn">sns</span>
</pre></div>

     </div>
</div>
</div>
</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&#160;[2]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor">
     <div class="CodeMirror cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">Raisin</span> <span class="o">=</span><span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="s1">&#39;./raisin_dataset.csv&#39;</span><span class="p">)</span>
<span class="n">Raisin</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>

     </div>
</div>
</div>
</div>

<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>


<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt">Out[2]:</div>



<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output jp-OutputArea-executeResult">
<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Area</th>
      <th>MajorAxisLength</th>
      <th>MinorAxisLength</th>
      <th>Eccentricity</th>
      <th>ConvexArea</th>
      <th>Extent</th>
      <th>Perimeter</th>
      <th>Class</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>87524</td>
      <td>442.246011</td>
      <td>253.291155</td>
      <td>0.819738</td>
      <td>90546</td>
      <td>0.758651</td>
      <td>1184.040</td>
      <td>Kecimen</td>
    </tr>
    <tr>
      <th>1</th>
      <td>75166</td>
      <td>406.690687</td>
      <td>243.032436</td>
      <td>0.801805</td>
      <td>78789</td>
      <td>0.684130</td>
      <td>1121.786</td>
      <td>Kecimen</td>
    </tr>
    <tr>
      <th>2</th>
      <td>90856</td>
      <td>442.267048</td>
      <td>266.328318</td>
      <td>0.798354</td>
      <td>93717</td>
      <td>0.637613</td>
      <td>1208.575</td>
      <td>Kecimen</td>
    </tr>
    <tr>
      <th>3</th>
      <td>45928</td>
      <td>286.540559</td>
      <td>208.760042</td>
      <td>0.684989</td>
      <td>47336</td>
      <td>0.699599</td>
      <td>844.162</td>
      <td>Kecimen</td>
    </tr>
    <tr>
      <th>4</th>
      <td>79408</td>
      <td>352.190770</td>
      <td>290.827533</td>
      <td>0.564011</td>
      <td>81463</td>
      <td>0.792772</td>
      <td>1073.251</td>
      <td>Kecimen</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>

</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&#160;[3]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor">
     <div class="CodeMirror cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">Raisin</span><span class="o">.</span><span class="n">describe</span><span class="p">()</span>
</pre></div>

     </div>
</div>
</div>
</div>

<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>


<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt">Out[3]:</div>



<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output jp-OutputArea-executeResult">
<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Area</th>
      <th>MajorAxisLength</th>
      <th>MinorAxisLength</th>
      <th>Eccentricity</th>
      <th>ConvexArea</th>
      <th>Extent</th>
      <th>Perimeter</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>900.000000</td>
      <td>900.000000</td>
      <td>900.000000</td>
      <td>900.000000</td>
      <td>900.000000</td>
      <td>900.000000</td>
      <td>900.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>87804.127778</td>
      <td>430.929950</td>
      <td>254.488133</td>
      <td>0.781542</td>
      <td>91186.090000</td>
      <td>0.699508</td>
      <td>1165.906636</td>
    </tr>
    <tr>
      <th>std</th>
      <td>39002.111390</td>
      <td>116.035121</td>
      <td>49.988902</td>
      <td>0.090318</td>
      <td>40769.290132</td>
      <td>0.053468</td>
      <td>273.764315</td>
    </tr>
    <tr>
      <th>min</th>
      <td>25387.000000</td>
      <td>225.629541</td>
      <td>143.710872</td>
      <td>0.348730</td>
      <td>26139.000000</td>
      <td>0.379856</td>
      <td>619.074000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>59348.000000</td>
      <td>345.442898</td>
      <td>219.111126</td>
      <td>0.741766</td>
      <td>61513.250000</td>
      <td>0.670869</td>
      <td>966.410750</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>78902.000000</td>
      <td>407.803951</td>
      <td>247.848409</td>
      <td>0.798846</td>
      <td>81651.000000</td>
      <td>0.707367</td>
      <td>1119.509000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>105028.250000</td>
      <td>494.187014</td>
      <td>279.888575</td>
      <td>0.842571</td>
      <td>108375.750000</td>
      <td>0.734991</td>
      <td>1308.389750</td>
    </tr>
    <tr>
      <th>max</th>
      <td>235047.000000</td>
      <td>997.291941</td>
      <td>492.275279</td>
      <td>0.962124</td>
      <td>278217.000000</td>
      <td>0.835455</td>
      <td>2697.753000</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>

</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&#160;[4]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor">
     <div class="CodeMirror cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#Class Balance</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Class Split&#39;</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="n">Raisin</span><span class="p">[</span><span class="s1">&#39;Class&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">value_counts</span><span class="p">())</span>
<span class="n">Raisin</span><span class="p">[</span><span class="s1">&#39;Class&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">value_counts</span><span class="p">()</span><span class="o">.</span><span class="n">plot</span><span class="o">.</span><span class="n">bar</span><span class="p">(</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">10</span><span class="p">,</span><span class="mi">4</span><span class="p">),</span><span class="n">title</span><span class="o">=</span><span class="s1">&#39;Classes Split for Dataset&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;Classes&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;Count&#39;</span><span class="p">)</span>
</pre></div>

     </div>
</div>
</div>
</div>

<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>


<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt"></div>


<div class="jp-RenderedText jp-OutputArea-output">
<pre>Class Split
Kecimen    450
Besni      450
Name: Class, dtype: int64
</pre>
</div>
</div>

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt">Out[4]:</div>




<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult">
<pre>Text(0, 0.5, &#39;Count&#39;)</pre>
</div>

</div>

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt"></div>




<div class="jp-RenderedImage jp-OutputArea-output">
<img src="javascript://"/>
</div>

</div>

</div>

</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&#160;[5]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor">
     <div class="CodeMirror cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#Define x and y variable</span>
<span class="n">x</span> <span class="o">=</span> <span class="n">Raisin</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="s1">&#39;Class&#39;</span><span class="p">,</span><span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span><span class="o">.</span><span class="n">to_numpy</span><span class="p">()</span>
<span class="n">y</span> <span class="o">=</span> <span class="n">Raisin</span><span class="p">[</span><span class="s1">&#39;Class&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">to_numpy</span><span class="p">()</span>

<span class="c1"># Create Train and Test Datasets</span>
<span class="kn">from</span> <span class="nn">sklearn.model_selection</span> <span class="kn">import</span> <span class="n">train_test_split</span>
<span class="n">x_train</span><span class="p">,</span> <span class="n">x_test</span><span class="p">,</span> <span class="n">y_train</span><span class="p">,</span> <span class="n">y_test</span> <span class="o">=</span> <span class="n">train_test_split</span><span class="p">(</span><span class="n">x</span><span class="p">,</span> <span class="n">y</span><span class="p">,</span> <span class="n">test_size</span><span class="o">=</span><span class="mf">0.20</span><span class="p">,</span><span class="n">stratify</span><span class="o">=</span><span class="n">y</span><span class="p">,</span><span class="n">random_state</span><span class="o">=</span><span class="mi">100</span><span class="p">)</span>

<span class="c1">#Scale the Data</span>
<span class="kn">from</span> <span class="nn">sklearn.preprocessing</span> <span class="kn">import</span> <span class="n">StandardScaler</span>
<span class="n">sc</span> <span class="o">=</span> <span class="n">StandardScaler</span><span class="p">()</span>
<span class="n">x_train2</span> <span class="o">=</span> <span class="n">sc</span><span class="o">.</span><span class="n">fit_transform</span><span class="p">(</span><span class="n">x_train</span><span class="p">)</span>
<span class="n">x_test2</span> <span class="o">=</span> <span class="n">sc</span><span class="o">.</span><span class="n">transform</span><span class="p">(</span><span class="n">x_test</span><span class="p">)</span>

<span class="c1">#Model</span>
<span class="kn">from</span> <span class="nn">sklearn.linear_model</span> <span class="kn">import</span> <span class="n">LogisticRegression</span>
</pre></div>

     </div>
</div>
</div>
</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&#160;[6]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor">
     <div class="CodeMirror cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#Base Logistical Regression Model</span>
<span class="kn">from</span> <span class="nn">sklearn.metrics</span> <span class="kn">import</span> <span class="n">classification_report</span><span class="p">,</span> <span class="n">confusion_matrix</span>  

<span class="k">for</span> <span class="n">name</span><span class="p">,</span><span class="n">method</span> <span class="ow">in</span> <span class="p">[(</span><span class="s1">&#39;LogReg&#39;</span><span class="p">,</span> <span class="n">LogisticRegression</span><span class="p">(</span><span class="n">solver</span><span class="o">=</span><span class="s1">&#39;lbfgs&#39;</span><span class="p">,</span><span class="n">class_weight</span><span class="o">=</span><span class="s1">&#39;balanced&#39;</span><span class="p">,</span>
                                               <span class="n">random_state</span><span class="o">=</span><span class="mi">100</span><span class="p">))]:</span> 
    <span class="n">method</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">x_train2</span><span class="p">,</span><span class="n">y_train</span><span class="p">)</span>
    <span class="n">predict</span> <span class="o">=</span> <span class="n">method</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">x_test2</span><span class="p">)</span>
    <span class="nb">print</span><span class="p">(</span><span class="s1">&#39;</span><span class="se">\n</span><span class="s1">Estimator: </span><span class="si">{}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">name</span><span class="p">))</span> 
    <span class="nb">print</span><span class="p">(</span><span class="n">confusion_matrix</span><span class="p">(</span><span class="n">y_test</span><span class="p">,</span><span class="n">predict</span><span class="p">))</span>  
    <span class="nb">print</span><span class="p">(</span><span class="n">classification_report</span><span class="p">(</span><span class="n">y_test</span><span class="p">,</span><span class="n">predict</span><span class="p">))</span>
</pre></div>

     </div>
</div>
</div>
</div>

<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>


<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt"></div>


<div class="jp-RenderedText jp-OutputArea-output">
<pre>
Estimator: LogReg
[[76 14]
 [12 78]]
              precision    recall  f1-score   support

       Besni       0.86      0.84      0.85        90
     Kecimen       0.85      0.87      0.86        90

    accuracy                           0.86       180
   macro avg       0.86      0.86      0.86       180
weighted avg       0.86      0.86      0.86       180

</pre>
</div>
</div>

</div>

</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&#160;[7]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor">
     <div class="CodeMirror cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#Construct some pipelines </span>
<span class="kn">from</span> <span class="nn">sklearn.pipeline</span> <span class="kn">import</span> <span class="n">Pipeline</span>
<span class="kn">from</span> <span class="nn">sklearn.preprocessing</span> <span class="kn">import</span> <span class="n">StandardScaler</span>

<span class="c1">#Create Pipeline</span>

<span class="n">pipeline</span> <span class="o">=</span><span class="p">[]</span>

<span class="n">pipe_logreg</span> <span class="o">=</span> <span class="n">Pipeline</span><span class="p">([(</span><span class="s1">&#39;scl&#39;</span><span class="p">,</span> <span class="n">StandardScaler</span><span class="p">()),</span>
                    <span class="p">(</span><span class="s1">&#39;clf&#39;</span><span class="p">,</span> <span class="n">LogisticRegression</span><span class="p">(</span><span class="n">solver</span><span class="o">=</span><span class="s1">&#39;lbfgs&#39;</span><span class="p">,</span><span class="n">class_weight</span><span class="o">=</span><span class="s1">&#39;balanced&#39;</span><span class="p">,</span>
                                               <span class="n">random_state</span><span class="o">=</span><span class="mi">100</span><span class="p">))])</span>
<span class="n">pipeline</span><span class="o">.</span><span class="n">insert</span><span class="p">(</span><span class="mi">0</span><span class="p">,</span><span class="n">pipe_logreg</span><span class="p">)</span>

<span class="c1">#Set grid search params </span>

<span class="n">modelpara</span> <span class="o">=</span><span class="p">[]</span>

<span class="n">param_gridlogreg</span> <span class="o">=</span> <span class="p">{</span><span class="s1">&#39;clf__C&#39;</span><span class="p">:</span> <span class="p">[</span><span class="mf">0.01</span><span class="p">,</span> <span class="mf">0.1</span><span class="p">,</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">10</span><span class="p">,</span> <span class="mi">100</span><span class="p">],</span> 
                    <span class="s1">&#39;clf__penalty&#39;</span><span class="p">:</span> <span class="p">[</span><span class="s1">&#39;l2&#39;</span><span class="p">]}</span>
<span class="n">modelpara</span><span class="o">.</span><span class="n">insert</span><span class="p">(</span><span class="mi">0</span><span class="p">,</span><span class="n">param_gridlogreg</span><span class="p">)</span>
</pre></div>

     </div>
</div>
</div>
</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&#160;[8]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor">
     <div class="CodeMirror cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="kn">from</span> <span class="nn">sklearn.model_selection</span> <span class="kn">import</span> <span class="n">learning_curve</span>

<span class="k">def</span> <span class="nf">plot_learning_curves</span><span class="p">(</span><span class="n">model</span><span class="p">):</span>
    <span class="n">train_sizes</span><span class="p">,</span> <span class="n">train_scores</span><span class="p">,</span> <span class="n">test_scores</span> <span class="o">=</span> <span class="n">learning_curve</span><span class="p">(</span><span class="n">estimator</span><span class="o">=</span><span class="n">model</span><span class="p">,</span>
                                                            <span class="n">X</span><span class="o">=</span><span class="n">x_train</span><span class="p">,</span> 
                                                            <span class="n">y</span><span class="o">=</span><span class="n">y_train</span><span class="p">,</span>
                                                            <span class="n">train_sizes</span><span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">linspace</span><span class="p">(</span><span class="mf">0.1</span><span class="p">,</span> <span class="mf">1.0</span><span class="p">,</span> <span class="mi">10</span><span class="p">),</span>
                                                            <span class="n">cv</span><span class="o">=</span><span class="mi">10</span><span class="p">,</span>
                                                            <span class="n">scoring</span><span class="o">=</span><span class="s1">&#39;recall_weighted&#39;</span><span class="p">,</span><span class="n">random_state</span><span class="o">=</span><span class="mi">100</span><span class="p">)</span>
    <span class="n">train_mean</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">mean</span><span class="p">(</span><span class="n">train_scores</span><span class="p">,</span> <span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span>
    <span class="n">train_std</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">std</span><span class="p">(</span><span class="n">train_scores</span><span class="p">,</span> <span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span>
    <span class="n">test_mean</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">mean</span><span class="p">(</span><span class="n">test_scores</span><span class="p">,</span> <span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span>
    <span class="n">test_std</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">std</span><span class="p">(</span><span class="n">test_scores</span><span class="p">,</span> <span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span>
    
    <span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">train_sizes</span><span class="p">,</span> <span class="n">train_mean</span><span class="p">,</span><span class="n">color</span><span class="o">=</span><span class="s1">&#39;blue&#39;</span><span class="p">,</span> <span class="n">marker</span><span class="o">=</span><span class="s1">&#39;o&#39;</span><span class="p">,</span> 
             <span class="n">markersize</span><span class="o">=</span><span class="mi">5</span><span class="p">,</span> <span class="n">label</span><span class="o">=</span><span class="s1">&#39;training recall&#39;</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">fill_between</span><span class="p">(</span><span class="n">train_sizes</span><span class="p">,</span> <span class="n">train_mean</span> <span class="o">+</span> <span class="n">train_std</span><span class="p">,</span> <span class="n">train_mean</span> <span class="o">-</span> <span class="n">train_std</span><span class="p">,</span>
                     <span class="n">alpha</span><span class="o">=</span><span class="mf">0.15</span><span class="p">,</span> <span class="n">color</span><span class="o">=</span><span class="s1">&#39;blue&#39;</span><span class="p">)</span>

    <span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">train_sizes</span><span class="p">,</span> <span class="n">test_mean</span><span class="p">,</span> <span class="n">color</span><span class="o">=</span><span class="s1">&#39;green&#39;</span><span class="p">,</span> <span class="n">linestyle</span><span class="o">=</span><span class="s1">&#39;--&#39;</span><span class="p">,</span> <span class="n">marker</span><span class="o">=</span><span class="s1">&#39;s&#39;</span><span class="p">,</span> <span class="n">markersize</span><span class="o">=</span><span class="mi">5</span><span class="p">,</span>
             <span class="n">label</span><span class="o">=</span><span class="s1">&#39;validation recall&#39;</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">fill_between</span><span class="p">(</span><span class="n">train_sizes</span><span class="p">,</span> <span class="n">test_mean</span> <span class="o">+</span> <span class="n">test_std</span><span class="p">,</span> <span class="n">test_mean</span> <span class="o">-</span> <span class="n">test_std</span><span class="p">,</span>
                     <span class="n">alpha</span><span class="o">=</span><span class="mf">0.15</span><span class="p">,</span> <span class="n">color</span><span class="o">=</span><span class="s1">&#39;green&#39;</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">grid</span><span class="p">(</span><span class="kc">True</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;Number of training samples&#39;</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;Recall&#39;</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">legend</span><span class="p">(</span><span class="n">loc</span><span class="o">=</span><span class="s1">&#39;best&#39;</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">ylim</span><span class="p">([</span><span class="mf">0.5</span><span class="p">,</span> <span class="mf">1.01</span><span class="p">])</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre></div>

     </div>
</div>
</div>
</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&#160;[9]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor">
     <div class="CodeMirror cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Logisistic Regression - Learning Curve&#39;</span><span class="p">)</span>
<span class="n">plot_learning_curves</span><span class="p">(</span><span class="n">pipe_logreg</span><span class="p">)</span>
</pre></div>

     </div>
</div>
</div>
</div>

<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>


<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt"></div>


<div class="jp-RenderedText jp-OutputArea-output">
<pre>Logisistic Regression - Learning Curve
</pre>
</div>
</div>

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt"></div>




<div class="jp-RenderedImage jp-OutputArea-output">
<img src="javascript://"/>
</div>

</div>

</div>

</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&#160;[10]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor">
     <div class="CodeMirror cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="kn">from</span> <span class="nn">mlxtend.evaluate</span> <span class="kn">import</span> <span class="n">bias_variance_decomp</span>

<span class="c1">#Convert Object columns to numeric</span>
<span class="kn">from</span> <span class="nn">sklearn.preprocessing</span> <span class="kn">import</span> <span class="n">LabelEncoder</span>
<span class="n">encoder</span> <span class="o">=</span> <span class="n">LabelEncoder</span><span class="p">()</span>
<span class="n">ytestConv</span> <span class="o">=</span> <span class="n">encoder</span><span class="o">.</span><span class="n">fit_transform</span><span class="p">(</span><span class="n">y_test</span><span class="p">)</span>
<span class="n">ytrainConv</span> <span class="o">=</span> <span class="n">encoder</span><span class="o">.</span><span class="n">fit_transform</span><span class="p">(</span><span class="n">y_train</span><span class="p">)</span>

<span class="c1">#Bias Variance Script</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Bias Variance Trade-Off&#39;</span><span class="p">)</span>
<span class="k">for</span> <span class="n">name</span><span class="p">,</span><span class="n">method</span> <span class="ow">in</span><span class="p">[(</span><span class="s1">&#39;Multi-Logistical Model&#39;</span><span class="p">,</span><span class="n">pipe_logreg</span><span class="p">)]:</span>        
    <span class="n">avg_expected_loss</span><span class="p">,</span> <span class="n">avg_bias</span><span class="p">,</span> <span class="n">avg_var</span> <span class="o">=</span> <span class="n">bias_variance_decomp</span><span class="p">(</span>
        <span class="n">method</span><span class="p">,</span> <span class="n">x_train2</span><span class="p">,</span> <span class="n">ytrainConv</span><span class="p">,</span> <span class="n">x_test2</span><span class="p">,</span> <span class="n">ytestConv</span><span class="p">,</span> 
        <span class="n">loss</span><span class="o">=</span><span class="s1">&#39;0-1_loss&#39;</span><span class="p">,</span>
        <span class="n">random_seed</span><span class="o">=</span><span class="mi">100</span><span class="p">)</span>
    <span class="nb">print</span><span class="p">(</span><span class="s1">&#39;</span><span class="se">\n</span><span class="s1">Estimator: </span><span class="si">{}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">name</span><span class="p">))</span> 
    <span class="nb">print</span><span class="p">(</span><span class="s1">&#39;</span><span class="se">\n</span><span class="s1">Average Bias: </span><span class="si">{:.2f}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">avg_bias</span><span class="p">))</span>
    <span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Average Variance: </span><span class="si">{:.2f}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">avg_var</span><span class="p">))</span>
</pre></div>

     </div>
</div>
</div>
</div>

<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>


<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt"></div>


<div class="jp-RenderedText jp-OutputArea-output">
<pre>Bias Variance Trade-Off

Estimator: Multi-Logistical Model

Average Bias: 0.14
Average Variance: 0.01
</pre>
</div>
</div>

</div>

</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&#160;[11]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor">
     <div class="CodeMirror cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="kn">from</span> <span class="nn">sklearn.model_selection</span> <span class="kn">import</span> <span class="n">RepeatedKFold</span>
<span class="kn">from</span> <span class="nn">sklearn.model_selection</span> <span class="kn">import</span> <span class="n">cross_val_score</span>

<span class="n">models</span><span class="o">=</span><span class="p">[]</span>
<span class="n">models</span><span class="o">.</span><span class="n">append</span><span class="p">((</span><span class="s1">&#39;Logistic Regression&#39;</span><span class="p">,</span><span class="n">pipe_logreg</span><span class="p">))</span>

<span class="c1">#Model Evaluation</span>
<span class="n">results</span> <span class="o">=</span><span class="p">[]</span>
<span class="n">names</span><span class="o">=</span><span class="p">[]</span>
<span class="n">scoring</span> <span class="o">=</span><span class="s1">&#39;recall_weighted&#39;</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Model Evaluation - Recall Weighted&#39;</span><span class="p">)</span>
<span class="k">for</span> <span class="n">name</span><span class="p">,</span> <span class="n">model</span> <span class="ow">in</span> <span class="n">models</span><span class="p">:</span>
    <span class="n">rkf</span><span class="o">=</span><span class="n">RepeatedKFold</span><span class="p">(</span><span class="n">n_splits</span><span class="o">=</span><span class="mi">10</span><span class="p">,</span> <span class="n">n_repeats</span><span class="o">=</span><span class="mi">5</span><span class="p">,</span> <span class="n">random_state</span><span class="o">=</span><span class="mi">100</span><span class="p">)</span>
    <span class="n">cv_results</span> <span class="o">=</span> <span class="n">cross_val_score</span><span class="p">(</span><span class="n">model</span><span class="p">,</span><span class="n">x_train</span><span class="p">,</span><span class="n">y_train</span><span class="p">,</span><span class="n">cv</span><span class="o">=</span><span class="n">rkf</span><span class="p">,</span><span class="n">scoring</span><span class="o">=</span><span class="n">scoring</span><span class="p">)</span>
    <span class="n">results</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">cv_results</span><span class="p">)</span>
    <span class="n">names</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">name</span><span class="p">)</span>
    <span class="nb">print</span><span class="p">(</span><span class="s1">&#39;</span><span class="si">{}</span><span class="s1"> </span><span class="si">{:.2f}</span><span class="s1"> +/- </span><span class="si">{:.2f}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">name</span><span class="p">,</span><span class="n">cv_results</span><span class="o">.</span><span class="n">mean</span><span class="p">(),</span><span class="n">cv_results</span><span class="o">.</span><span class="n">std</span><span class="p">()))</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;</span><span class="se">\n</span><span class="s1">&#39;</span><span class="p">)</span>

<span class="n">fig</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">figure</span><span class="p">(</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">5</span><span class="p">,</span><span class="mi">5</span><span class="p">))</span>
<span class="n">fig</span><span class="o">.</span><span class="n">suptitle</span><span class="p">(</span><span class="s1">&#39;Boxplot View&#39;</span><span class="p">)</span>
<span class="n">ax</span> <span class="o">=</span> <span class="n">fig</span><span class="o">.</span><span class="n">add_subplot</span><span class="p">(</span><span class="mi">111</span><span class="p">)</span>
<span class="n">sns</span><span class="o">.</span><span class="n">boxplot</span><span class="p">(</span><span class="n">data</span><span class="o">=</span><span class="n">results</span><span class="p">)</span>
<span class="n">ax</span><span class="o">.</span><span class="n">set_xticklabels</span><span class="p">(</span><span class="n">names</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;Recall&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;Model&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre></div>

     </div>
</div>
</div>
</div>

<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>


<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt"></div>


<div class="jp-RenderedText jp-OutputArea-output">
<pre>Model Evaluation - Recall Weighted
Logistic Regression 0.87 +/- 0.04


</pre>
</div>
</div>

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt"></div>




<div class="jp-RenderedImage jp-OutputArea-output">
<img src="javascript://"/>
</div>

</div>

</div>

</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&#160;[12]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor">
     <div class="CodeMirror cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="kn">from</span> <span class="nn">sklearn.model_selection</span> <span class="kn">import</span> <span class="n">GridSearchCV</span>
<span class="kn">from</span> <span class="nn">sklearn.metrics</span> <span class="kn">import</span> <span class="n">classification_report</span><span class="p">,</span> <span class="n">confusion_matrix</span>  

<span class="k">def</span> <span class="nf">Gridsearch_cv</span><span class="p">(</span><span class="n">model</span><span class="p">,</span> <span class="n">params</span><span class="p">):</span>
    
    <span class="c1">#Cross-validation Function</span>
    <span class="n">cv2</span><span class="o">=</span><span class="n">RepeatedKFold</span><span class="p">(</span><span class="n">n_splits</span><span class="o">=</span><span class="mi">10</span><span class="p">,</span> <span class="n">n_repeats</span><span class="o">=</span><span class="mi">5</span><span class="p">,</span> <span class="n">random_state</span><span class="o">=</span><span class="mi">100</span><span class="p">)</span>
        
    <span class="c1">#GridSearch CV</span>
    <span class="n">gs_clf</span> <span class="o">=</span> <span class="n">GridSearchCV</span><span class="p">(</span><span class="n">model</span><span class="p">,</span> <span class="n">params</span><span class="p">,</span> <span class="n">cv</span><span class="o">=</span><span class="n">cv2</span><span class="p">,</span><span class="n">scoring</span><span class="o">=</span><span class="s1">&#39;recall_weighted&#39;</span><span class="p">)</span>
    <span class="n">gs_clf</span> <span class="o">=</span> <span class="n">gs_clf</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">x_train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">)</span>
    <span class="n">model</span> <span class="o">=</span> <span class="n">gs_clf</span><span class="o">.</span><span class="n">best_estimator_</span>
    
    <span class="c1"># Use best model and test data for final evaluation</span>
    <span class="n">y_pred</span> <span class="o">=</span> <span class="n">model</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">x_test</span><span class="p">)</span>
    
    <span class="c1">#Identify Best Parameters to Optimize the Model</span>
    <span class="n">bestpara</span><span class="o">=</span><span class="nb">str</span><span class="p">(</span><span class="n">gs_clf</span><span class="o">.</span><span class="n">best_params_</span><span class="p">)</span>
    
    <span class="c1">#Output Heading</span>
    <span class="nb">print</span><span class="p">(</span><span class="s1">&#39;</span><span class="se">\n</span><span class="s1">Optimized Model&#39;</span><span class="p">)</span>
    <span class="nb">print</span><span class="p">(</span><span class="s1">&#39;</span><span class="se">\n</span><span class="s1">Model Name:&#39;</span><span class="p">,</span><span class="nb">str</span><span class="p">(</span><span class="n">pipeline</span><span class="o">.</span><span class="n">named_steps</span><span class="p">[</span><span class="s1">&#39;clf&#39;</span><span class="p">]))</span>
        
    <span class="c1">#Output Validation Statistics</span>
    <span class="n">target_names</span><span class="o">=</span><span class="p">[</span><span class="s1">&#39;Outcome 0&#39;</span><span class="p">,</span><span class="s1">&#39;Outcome 1&#39;</span><span class="p">]</span>
    <span class="nb">print</span><span class="p">(</span><span class="s1">&#39;</span><span class="se">\n</span><span class="s1">Best Parameters:&#39;</span><span class="p">,</span><span class="n">bestpara</span><span class="p">)</span>
    <span class="nb">print</span><span class="p">(</span><span class="s1">&#39;</span><span class="se">\n</span><span class="s1">&#39;</span><span class="p">,</span> <span class="n">confusion_matrix</span><span class="p">(</span><span class="n">y_test</span><span class="p">,</span><span class="n">y_pred</span><span class="p">))</span>  
    <span class="nb">print</span><span class="p">(</span><span class="s1">&#39;</span><span class="se">\n</span><span class="s1">&#39;</span><span class="p">,</span><span class="n">classification_report</span><span class="p">(</span><span class="n">y_test</span><span class="p">,</span><span class="n">y_pred</span><span class="p">,</span><span class="n">target_names</span><span class="o">=</span><span class="n">target_names</span><span class="p">))</span> 
        
    <span class="c1">#Transform the variables into binary (0,1) - ROC Curve</span>
    <span class="kn">from</span> <span class="nn">sklearn</span> <span class="kn">import</span> <span class="n">preprocessing</span>
    <span class="n">Forecast1</span><span class="o">=</span><span class="n">pd</span><span class="o">.</span><span class="n">DataFrame</span><span class="p">(</span><span class="n">y_pred</span><span class="p">)</span>
    <span class="n">Outcome1</span><span class="o">=</span><span class="n">pd</span><span class="o">.</span><span class="n">DataFrame</span><span class="p">(</span><span class="n">y_test</span><span class="p">)</span>
    <span class="n">lb1</span> <span class="o">=</span> <span class="n">preprocessing</span><span class="o">.</span><span class="n">LabelBinarizer</span><span class="p">()</span>
    <span class="n">OutcomeB1</span> <span class="o">=</span><span class="n">lb1</span><span class="o">.</span><span class="n">fit_transform</span><span class="p">(</span><span class="n">Outcome1</span><span class="p">)</span>
    <span class="n">ForecastB1</span> <span class="o">=</span> <span class="n">lb1</span><span class="o">.</span><span class="n">fit_transform</span><span class="p">(</span><span class="n">Forecast1</span><span class="p">)</span>
    
    <span class="c1">#Setup the ROC Curve</span>
    <span class="kn">from</span> <span class="nn">sklearn.metrics</span> <span class="kn">import</span> <span class="n">roc_curve</span><span class="p">,</span> <span class="n">auc</span>
    <span class="kn">from</span> <span class="nn">sklearn</span> <span class="kn">import</span> <span class="n">metrics</span>
    <span class="n">fpr</span><span class="p">,</span> <span class="n">tpr</span><span class="p">,</span> <span class="n">threshold</span> <span class="o">=</span> <span class="n">metrics</span><span class="o">.</span><span class="n">roc_curve</span><span class="p">(</span><span class="n">OutcomeB1</span><span class="p">,</span> <span class="n">ForecastB1</span><span class="p">)</span>
    <span class="n">roc_auc</span> <span class="o">=</span> <span class="n">metrics</span><span class="o">.</span><span class="n">auc</span><span class="p">(</span><span class="n">fpr</span><span class="p">,</span> <span class="n">tpr</span><span class="p">)</span>
    <span class="nb">print</span><span class="p">(</span><span class="s1">&#39;ROC Curve&#39;</span><span class="p">)</span>
    <span class="c1">#Plot the ROC Curve</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">&#39;Receiver Operating Characteristic&#39;</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">fpr</span><span class="p">,</span> <span class="n">tpr</span><span class="p">,</span> <span class="s1">&#39;b&#39;</span><span class="p">,</span> <span class="n">label</span> <span class="o">=</span> <span class="s1">&#39;AUC = </span><span class="si">%0.2f</span><span class="s1">&#39;</span> <span class="o">%</span> <span class="n">roc_auc</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">legend</span><span class="p">(</span><span class="n">loc</span> <span class="o">=</span> <span class="s1">&#39;lower right&#39;</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">([</span><span class="mi">0</span><span class="p">,</span> <span class="mi">1</span><span class="p">],</span> <span class="p">[</span><span class="mi">0</span><span class="p">,</span> <span class="mi">1</span><span class="p">],</span><span class="s1">&#39;r--&#39;</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">xlim</span><span class="p">([</span><span class="mi">0</span><span class="p">,</span> <span class="mi">1</span><span class="p">])</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">ylim</span><span class="p">([</span><span class="mi">0</span><span class="p">,</span> <span class="mi">1</span><span class="p">])</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;True Positive Rate&#39;</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;False Positive Rate&#39;</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre></div>

     </div>
</div>
</div>
</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&#160;[13]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor">
     <div class="CodeMirror cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="k">for</span> <span class="n">pipeline</span><span class="p">,</span> <span class="n">modelpara</span> <span class="ow">in</span> <span class="nb">zip</span><span class="p">(</span><span class="n">pipeline</span><span class="p">,</span><span class="n">modelpara</span><span class="p">):</span>
    <span class="n">Gridsearch_cv</span><span class="p">(</span><span class="n">pipeline</span><span class="p">,</span><span class="n">modelpara</span><span class="p">)</span>
</pre></div>

     </div>
</div>
</div>
</div>

<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>


<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt"></div>


<div class="jp-RenderedText jp-OutputArea-output">
<pre>
Optimized Model

Model Name: LogisticRegression(class_weight=&#39;balanced&#39;, random_state=100)

Best Parameters: {&#39;clf__C&#39;: 0.01, &#39;clf__penalty&#39;: &#39;l2&#39;}

 [[73 17]
 [12 78]]

               precision    recall  f1-score   support

   Outcome 0       0.86      0.81      0.83        90
   Outcome 1       0.82      0.87      0.84        90

    accuracy                           0.84       180
   macro avg       0.84      0.84      0.84       180
weighted avg       0.84      0.84      0.84       180

ROC Curve
</pre>
</div>
</div>

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt"></div>




<div class="jp-RenderedImage jp-OutputArea-output">
<img src="javascript://"/>
</div>

</div>

</div>

</div>

</div>









<script type="module" src="https://s.brightspace.com/lib/bsi/2024.10.209/unbundled/mathjax.js"></script><script type="text/javascript">document.addEventListener('DOMContentLoaded', function() {
						if (document.querySelector('math') || /\$\$|\\\(|\\\[|\\begin{|\\ref{|\\eqref{/.test(document.body.innerHTML)) {
							document.querySelectorAll('mspace[linebreak="newline"]').forEach(elm => {
								elm.setAttribute('style', 'display: block; height: 0.5rem;');
							});

							window.D2L.MathJax.loadMathJax({
								outputScale: 1.5,
								renderLatex: false,
								enableMML3Support: false
							});
						}
					});</script><script type="module" src="https://s.brightspace.com/lib/bsi/2024.10.209/unbundled/prism.js"></script><script type="text/javascript">document.addEventListener('DOMContentLoaded', function() {
					document.querySelectorAll('.d2l-code').forEach(code => {
						window.D2L.Prism.formatCodeElement(code);
					});
				});</script><script type="module" src="https://s.brightspace.com/lib/bsi/2024.10.209/unbundled/embeds.js"></script><script type="text/javascript">document.addEventListener('DOMContentLoaded', function() {
					window.D2L.EmbedRenderer.renderEmbeds(document.body);
				});</script></body></html>g CODE.html…]()
