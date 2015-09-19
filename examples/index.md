---
layout: page
title: Examples
excerpt: "Examples showing how to use metaknowledge to analyze data."
search_omit: true
---

<ul class="post-list">

  <li><article>
  <a href="{{ site.baseurl }}/examples/#Context">Context</a>
  </article></li>
  <li><article>
  <a href="{{ site.baseurl }}/examples/#Importing">Importing</a>
  </article></li>
  <li><article>
  <a href="{{ site.baseurl }}/examples/#Reading-Files">Reading Files</a>
  </article></li>
  <li><article>
  <a href="{{ site.baseurl }}/examples/#Record-object">Record object</a>
  </article></li>
  <li><article>
  <a href="{{ site.baseurl }}/examples/#RecordCollection-object">RecordCollection object</a>
  </article></li>
  <li><article>
  <a href="{{ site.baseurl }}/examples/#Citation-object">Citation object</a>
  </article></li>
  <li><article>
  <a href="{{ site.baseurl }}/examples/#Filtering">Filtering</a>
  </article></li>
  <li><article>
  <a href="{{ site.baseurl }}/examples/#Exporting-RecordCollections">Exporting RecordCollections</a>
  </article></li>
  <li><article>
  <a href="{{ site.baseurl }}/examples/#Making-a-co-citation-network">Making a co-citation network</a>
  </article></li>
  <li><article>
  <a href="{{ site.baseurl }}/examples/#Making-a-citation-network">Making a citation network</a>
  </article></li>
  <li><article>
  <a href="{{ site.baseurl }}/examples/#Making-a-co-author-network">Making a co-author network</a>
  </article></li>
  <li><article>
  <a href="{{ site.baseurl }}/examples/#Making-a-one-mode-network">Making a one-mode network</a>
  </article></li>
  <li><article>
  <a href="{{ site.baseurl }}/examples/#Making-a-two-mode-network">Making a two-mode network</a>
  </article></li>
  <li><article>
  <a href="{{ site.baseurl }}/examples/#Making-a-multi-mode-network">Making a multi-mode network</a>
  </article></li>
  <li><article>
  <a href="{{ site.baseurl }}/examples/#Post-processing-graphs">Post processing graphs</a>
  </article></li>
  <li><article>
  <a href="{{ site.baseurl }}/examples/#Exporting-graphs">Exporting graphs</a>
  </article></li>
</ul>

<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Context">Context<a class="anchor-link" href="#Context">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>{% comment %}</p>
<h1 id="Notes-for-those-who-downloaded-the-notebook">Notes for those who downloaded the notebook<a class="anchor-link" href="#Notes-for-those-who-downloaded-the-notebook">&#182;</a></h1><p>The notebook should just work as long as you put the sample file (<code>savedrecs.txt</code>) in the same directory as this file.</p>
<p>The one issue you will have is that the urls will not work. To make them work you will need to replace <code>{{ site.baseurl }}</code> with <code>http://networkslab.org/metaknowledge</code>, sorry about that.</p>
<p>{% endcomment %}</p>
<p><em>metaknowledge</em> is a python library for creating and analyzing scientific metadata. It uses records obtained from Web of Science (WOS) and mostly produces graphs. As it is intended to be usable by those who do not know much python. This page will be a short overview of its capabilities, to allow you to use it for your own work. For complete coverage of the package as well as install instructions read the full the documentation <a href="{{ site.baseurl }}/documentation">here</a>.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>This document was made from a <a href="https://jupyter.org">jupyter</a> notebook, if you know how to use them, you can download the notebook <a href="{{ site.baseurl }}/examples/metaknowledgeExamples.ipynb">here</a> and the sample file is <a href="{{ site.baseurl }}/examples/savedrecs.txt">here</a> if you wish to have an interactive version of this page. Now lets begin.</p>
<h1 id="Importing">Importing<a class="anchor-link" href="#Importing">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>First you need to import the <em>metaknowledge</em> package</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[1]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="kn">import</span> <span class="nn">metaknowledge</span> <span class="k">as</span> <span class="nn">mk</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>And you will often need the <a href="https://networkx.github.io/documentation/networkx-1.9.1/"><em>networkx</em></a> package</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[2]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="kn">import</span> <span class="nn">networkx</span> <span class="k">as</span> <span class="nn">nx</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>I am using <a href="http://matplotlib.org/"><em>matplotlib</em></a> to display the graphs and to make them look nice when displayed</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[3]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="k">as</span> <span class="nn">plt</span>
<span class="o">%</span><span class="k">matplotlib</span> inline
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><em>metaknowledge</em> also has a <em>matplotlib</em> based graph <a href="{{ site.baseurl }}/docs/visual#visual">visualizer</a></p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[4]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="kn">import</span> <span class="nn">metaknowledge.visual</span> <span class="k">as</span> <span class="nn">mkv</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><a href="http://pandas.pydata.org/"><em>pandas</em></a> is also used in one example</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[5]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="kn">import</span> <span class="nn">pandas</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Reading-Files">Reading Files<a class="anchor-link" href="#Reading-Files">&#182;</a></h1><p>The files from the Web of Science (WOS) can be loaded into a <a href="{{ site.baseurl }}/docs/RecordCollection#RecordCollection"><code>RecordCollections</code></a> by creating a <code>RecordCollection</code> with the path to the files given to it as a string.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[6]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">RC</span> <span class="o">=</span> <span class="n">mk</span><span class="o">.</span><span class="n">RecordCollection</span><span class="p">(</span><span class="s">&quot;savedrecs.txt&quot;</span><span class="p">)</span>
<span class="nb">repr</span><span class="p">(</span><span class="n">RC</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[6]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>&apos;savedrecs&apos;</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>You can also read a whole directory, in this case it is reading the current working directory</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[7]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">RC</span> <span class="o">=</span> <span class="n">mk</span><span class="o">.</span><span class="n">RecordCollection</span><span class="p">(</span><span class="s">&quot;.&quot;</span><span class="p">)</span>
<span class="nb">repr</span><span class="p">(</span><span class="n">RC</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[7]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>&apos;files-from-.&apos;</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><em>metaknowledge</em> can detect if a file is a valid WOS file or not and will read the entire directory and load only those that have the right header. You can also tell it to only read a certain type of file, by using the extension argument.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[8]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">RC</span> <span class="o">=</span> <span class="n">mk</span><span class="o">.</span><span class="n">RecordCollection</span><span class="p">(</span><span class="s">&quot;.&quot;</span><span class="p">,</span> <span class="n">extension</span> <span class="o">=</span> <span class="s">&quot;txt&quot;</span><span class="p">)</span>
<span class="nb">repr</span><span class="p">(</span><span class="n">RC</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[8]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>&apos;txt-files-from-.&apos;</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Now you have a <code>RecordCollection</code> composed of all the WOS records in the selected file(s).</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[9]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="nb">print</span><span class="p">(</span><span class="s">&quot;RC is a &quot;</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="n">RC</span><span class="p">))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>RC is a Collection of 32 records
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>You might have noticed I used two different ways to display the <code>RecordCollection</code>. <code>repr(RC)</code> will give you where <em>metaknowledge</em> thinks the collection came from. While <code>str(RC)</code> will give you a nice string containing the number of <code>Records</code>.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Record-object"><code>Record</code> object<a class="anchor-link" href="#Record-object">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><a href="{{ site.baseurl }}/docs/Record#Record"><code>Record</code></a> is an object that contains a simple WOS record, for example a journal article, book, or conference proceedings. They are what <a href="{{ site.baseurl }}/docs/RecordCollection#RecordCollection"><code>RecordCollections</code></a> contain. To see an individual <a href="{{ site.baseurl }}/docs/Record#Record"><code>Record</code></a> at random from a <code>RecordCollection</code> you can use <code>peak()</code></p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[10]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">R</span> <span class="o">=</span> <span class="n">RC</span><span class="o">.</span><span class="n">peak</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>A single <code>Record</code> can give you all the information it contains about its record. If for example you want its authors.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[11]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="nb">print</span><span class="p">(</span><span class="n">R</span><span class="o">.</span><span class="n">authorsFull</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="n">R</span><span class="o">.</span><span class="n">AF</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>[&apos;Zhang Zhi-Wei&apos;, &apos;Wen Ting-Dun&apos;, &apos;Zhang Ji-Long&apos;]
[&apos;Zhang Zhi-Wei&apos;, &apos;Wen Ting-Dun&apos;, &apos;Zhang Ji-Long&apos;]
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Converting a <code>Record</code> to a string will give its title</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[12]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="nb">print</span><span class="p">(</span><span class="n">R</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>A Novel Method for Enhancing Goos-Hanchen Shift in Total Internal Reflection
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>If you try to access a tag the <code>Record</code> does not have it will return <code>None</code></p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[13]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="nb">print</span><span class="p">(</span><span class="n">R</span><span class="o">.</span><span class="n">GP</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>None
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>There are two ways of getting each tag, one is using the WOS 2 letter abbreviation and the second is to use the human readable name. There is no standard for the human readable names, so they are specific to <em>metaknowledge</em>. To see how the WOS names map to the long names look at <a href="{{ site.baseurl }}/docs/tagFuncs#tagFuncs">tagFuncs</a>. If you want all the tags a <code>Record</code> has use <a href="({{ site.baseurl }}/docs/Record#activeTags"><code>activeTags()</code></a>.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[14]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="nb">print</span><span class="p">(</span><span class="n">R</span><span class="o">.</span><span class="n">activeTags</span><span class="p">())</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>[&apos;PT&apos;, &apos;AU&apos;, &apos;AF&apos;, &apos;TI&apos;, &apos;SO&apos;, &apos;LA&apos;, &apos;DT&apos;, &apos;ID&apos;, &apos;AB&apos;, &apos;C1&apos;, &apos;RP&apos;, &apos;EM&apos;, &apos;FU&apos;, &apos;FX&apos;, &apos;CR&apos;, &apos;NR&apos;, &apos;TC&apos;, &apos;Z9&apos;, &apos;PU&apos;, &apos;PI&apos;, &apos;PA&apos;, &apos;SN&apos;, &apos;J9&apos;, &apos;JI&apos;, &apos;PD&apos;, &apos;PY&apos;, &apos;VL&apos;, &apos;IS&apos;, &apos;AR&apos;, &apos;PG&apos;, &apos;WC&apos;, &apos;SC&apos;, &apos;GA&apos;, &apos;UT&apos;]
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="RecordCollection-object"><code>RecordCollection</code> object<a class="anchor-link" href="#RecordCollection-object">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><a href="{{ site.baseurl }}/docs/RecordCollection#RecordCollection"><code>RecordCollection</code></a> is the object that <em>metaknowledge</em> uses the most. It is your interface with the data you want.</p>
<p>To iterate over all of the <code>Records</code> you can use a for loop</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[15]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="k">for</span> <span class="n">R</span> <span class="ow">in</span> <span class="n">RC</span><span class="p">:</span>
    <span class="nb">print</span><span class="p">(</span><span class="n">R</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>A Novel Method for Enhancing Goos-Hanchen Shift in Total Internal Reflection
EXPERIMENTS IN PHENOMENOLOGICAL ELECTRODYNAMICS AND THE ELECTROMAGNETIC ENERGY-MOMENTUM TENSOR
NONLINEAR TOTALLY REFLECTING PRISM COUPLER - THERMOMECHANIC EFFECTS AND INTENSITY-DEPENDENT REFRACTIVE-INDEX OF THIN-FILMS
ANGULAR SPECTRUM AS AN ELECTRICAL NETWORK
Goos-Hanchen shift as a probe in evanescent slab waveguide sensors
GENERAL STUDY OF DISPLACEMENTS AT TOTAL REFLECTION
INTERNAL PHOTON IMPULSE OF DIELECTRIC AND ON COUPLE APPLIED TO ANISOTROPIC CRYSTAL
DISCUSSIONS OF PROBLEM OF PONDEROMOTIVE FORCES
Optical properties of nanostructured thin films
WHY ENERGY FLUX AND ABRAHAMS PHOTON MOMENTUM ARE MACROSCOPICALLY SUBSTITUTED FOR MOMENTUM DENSITY AND MINKOWSKIS PHOTON MOMENTUM
LONGITUDINAL AND TRANSVERSE DISPLACEMENTS OF A BOUNDED MICROWAVE BEAM AT TOTAL INTERNAL-REFLECTION
MECHANICAL INTERPRETATION OF SHIFTS IN TOTAL REFLECTION OF SPINNING PARTICLES
PREDICTION OF A RESONANCE-ENHANCED LASER-BEAM DISPLACEMENT AT TOTAL INTERNAL-REFLECTION IN SEMICONDUCTORS
Longitudinal and transverse effects of nonspecular reflection
EXCHANGED MOMENTUM BETWEEN MOVING ATOMS AND A SURFACE-WAVE - THEORY AND EXPERIMENT
SHIFTS OF COHERENT-LIGHT BEAMS ON REFLECTION AT PLANE INTERFACES BETWEEN ISOTROPIC MEDIA
DISPLACEMENT OF A TOTALLY REFLECTED LIGHT-BEAM - FILTERING OF POLARIZATION STATES AND AMPLIFICATION
Transverse displacement at total reflection near the grazing angle: a way to discriminate between theories
SPIN ANGULAR-MOMENTUM OF A FIELD INTERACTING WITH A PLANE INTERFACE
ASYMMETRICAL MOMENTUM-ENERGY TENSORS AND 6-COMPONENT ANGULAR-MOMENTUM IN PROBLEM CONCERNING 2 PHOTON MOMENTA AND MAGNETODYNAMIC EFFECT PROBLEM
CONSERVATION OF ANGULAR MOMENT WITH SIX COMPONENTS AND ASYMMETRICAL IMPULSE ENERGY TENSORS
Numerical study of the displacement of a three-dimensional Gaussian beam transmitted at total internal reflection. Near-field applications
THEORETICAL NOTES ON AMPLIFICATION OF TRANSVERSE SHIFT BY TOTAL REFLECTION ON MULTILAYERED SYSTEM
INTERFERENCE THEORY OF REFLECTION FROM MULTILAYERED MEDIA
Experimental observation of the Imbert-Fedorov transverse displacement after a single total reflection
SPIN ANGULAR-MOMENTUM OF A FIELD INTERACTING WITH A PLANE INTERFACE
Simple technique for measuring the Goos-Hanchen effect with polarization modulation and a position-sensitive detector
Goos-Hanchen and Imbert-Fedorov shifts for leaky guided modes
RESONANCE EFFECTS ON TOTAL INTERNAL-REFLECTION AND LATERAL (GOOS-HANCHEN) BEAM DISPLACEMENT AT THE INTERFACE BETWEEN NONLOCAL AND LOCAL DIELECTRIC
OBSERVATION OF SHIFTS IN TOTAL REFLECTION OF A LIGHT-BEAM BY A MULTILAYERED STRUCTURE
CALCULATION AND MEASUREMENT OF FORCES AND TORQUES APPLIED TO UNIAXIAL CRYSTAL BY EXTRAORDINARY WAVE
TRANSVERSE DISPLACEMENT OF A TOTALLY REFLECTED LIGHT-BEAM AND PHASE-SHIFT METHOD
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>The individual <code>Records</code> are index by their WOS numbers so you can access a specific one in the collection if you know its number.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[16]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">RC</span><span class="o">.</span><span class="n">getWOS</span><span class="p">(</span><span class="s">&quot;WOS:A1979GV55600001&quot;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[16]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>&lt;metaknowledge.record.Record at 0x111be06a0&gt;</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Citation-object"><code>Citation</code> object<a class="anchor-link" href="#Citation-object">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><a href="{{ site.baseurl }}/docs/Citation#Citation"><code>Citation</code></a> is an object to contain the results of parsing a citation. They can be created from a <code>Record</code></p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[17]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">Cite</span> <span class="o">=</span> <span class="n">R</span><span class="o">.</span><span class="n">createCitation</span><span class="p">()</span>
<span class="nb">print</span><span class="p">(</span><span class="n">Cite</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>CANALSFRAU D, 1975, NOUV REV OPT, V6, P203, DOI 10.1088/0335-7368/6/4/303
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><code>Citations</code> allow for the raw strings of citations to be manipulated easily by <em>metaknowledge</em>.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Filtering">Filtering<a class="anchor-link" href="#Filtering">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>The for loop shown above is the main way to filter a RecordCollection, that said there are a few builtin filters, e.g. <a href="{{ site.baseurl }}/docs/RecordCollection#yearSplit"><code>yearSplit()</code></a>, but the for loop is an easily generalized way of filtering that is relatively simple to read so it the main way you should filter. An example of the workflow is as follows:</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>First create a new RecordCollection</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[18]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">RCfiltered</span> <span class="o">=</span> <span class="n">mk</span><span class="o">.</span><span class="n">RecordCollection</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Then add the records that meet your condition, in this case that their title's start with <code>'A'</code></p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[19]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="k">for</span> <span class="n">R</span> <span class="ow">in</span> <span class="n">RC</span><span class="p">:</span>
    <span class="k">if</span> <span class="n">R</span><span class="o">.</span><span class="n">title</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span> <span class="o">==</span> <span class="s">&#39;A&#39;</span><span class="p">:</span>
        <span class="n">RCfiltered</span><span class="o">.</span><span class="n">addRec</span><span class="p">(</span><span class="n">R</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[20]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="nb">print</span><span class="p">(</span><span class="n">RCfiltered</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>Collection of 3 records
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Now you have a RecordCollection <code>RCfiltered</code> of all the <code>Records</code> whose titles begin with <code>'A'</code>.</p>
<p>One note about implementing this, the above code does not handle the case in which the title is missing i.e. <code>R.title</code> is <code>None</code>. You will have to deal with this on your own.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Two builtin functions to filter collections are <a href="{{ site.baseurl }}/docs/RecordCollection#yearSplit"><code>yearSplit()</code></a> and <a href="{{ site.baseurl }}/docs/RecordCollection#localCitesOf"><code>localCitesOf()</code></a>. To get a RecordCollection of all Records between 1970 and 1979:</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[21]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">RC70</span> <span class="o">=</span> <span class="n">RC</span><span class="o">.</span><span class="n">yearSplit</span><span class="p">(</span><span class="mi">1970</span><span class="p">,</span> <span class="mi">1979</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="n">RC70</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>Collection of 19 records
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>The second function <a href="{{ site.baseurl }}/docs/RecordCollection#localCitesOf"><code>localCitesOf()</code></a> takes in an object that a <a href="{{ site.baseurl }}/docs/Citation#Citation">Citation</a> can be created from and returns a RecordCollection of all the Records that cite it. So to see all the records that cite <code>"Yariv A., 1971, INTRO OPTICAL ELECTR"</code>.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[22]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">RCintroOpt</span> <span class="o">=</span> <span class="n">RC</span><span class="o">.</span><span class="n">localCitesOf</span><span class="p">(</span><span class="s">&quot;Yariv A., 1971, INTRO OPTICAL ELECTR&quot;</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="n">RCintroOpt</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>Collection of 1 records
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Exporting-RecordCollections">Exporting RecordCollections<a class="anchor-link" href="#Exporting-RecordCollections">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Now you have a filtered RecordCollection you can write it as a file with <a href="{{ site.baseurl }}/docs/RecordCollection#writeFile"><code>writeFile()</code></a></p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[23]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre> <span class="n">RCfiltered</span><span class="o">.</span><span class="n">writeFile</span><span class="p">(</span><span class="s">&quot;Records_Starting_with_A.txt&quot;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>The written file is identical to one of those produced by WOS.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>If you wish to have a more useful file use <a href="{{ site.baseurl }}/docs/RecordCollection#writeCSV"><code>writeCSV()</code></a> which creates a CSV file of all the tags as columns and the Records as rows. IF you only care about a few tags the <code>onlyTheseTags</code> argument allows you to control the tags.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[24]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">selectedTags</span> <span class="o">=</span> <span class="p">[</span><span class="s">&#39;TI&#39;</span><span class="p">,</span> <span class="s">&#39;UT&#39;</span><span class="p">,</span> <span class="s">&#39;CR&#39;</span><span class="p">,</span> <span class="s">&#39;AF&#39;</span><span class="p">]</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>This will give only the title, WOS number, citations, and authors.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[25]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">RCfiltered</span><span class="o">.</span><span class="n">writeCSV</span><span class="p">(</span><span class="s">&quot;Records_Starting_with_A.csv&quot;</span><span class="p">,</span> <span class="n">onlyTheseTags</span> <span class="o">=</span> <span class="n">selectedTags</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>The last export feature is for using <em>metaknowledge</em> with other packages, in particular <a href="http://pandas.pydata.org/"><em>pandas</em></a> but others should also work. <a href="{{ site.baseurl }}/docs/RecordCollection#makeDict"><code>makeDict()</code></a> creates a dictionary with tags as keys and lists as values with each index of the lists corresponding to a Record. <em>pandas</em> can accept these directly to make DataFrames.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[26]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">recDataFrame</span> <span class="o">=</span> <span class="n">pandas</span><span class="o">.</span><span class="n">DataFrame</span><span class="p">(</span><span class="n">RC</span><span class="o">.</span><span class="n">makeDict</span><span class="p">())</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Making-a-co-citation-network">Making a co-citation network<a class="anchor-link" href="#Making-a-co-citation-network">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>To make a basic co-citation network of Records use <a href="{{ site.baseurl }}/docs/RecordCollection#coCiteNetwork"><code>coCiteNetwork()</code></a>.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[27]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">coCites</span> <span class="o">=</span> <span class="n">RC</span><span class="o">.</span><span class="n">coCiteNetwork</span><span class="p">()</span>
<span class="nb">print</span><span class="p">(</span><span class="n">mk</span><span class="o">.</span><span class="n">graphStats</span><span class="p">(</span><span class="n">coCites</span><span class="p">,</span> <span class="n">makeString</span> <span class="o">=</span> <span class="k">True</span><span class="p">))</span> <span class="c">#makestring by default is True so it is not strictly necessary to include</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>The graph has 601 nodes, 19492 edges, 0 isolates, 4 self loops, a density of 0.108109 and a transitivity of 0.691662
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><a href="{{ site.baseurl }}/docs/metaknowledge#graphStats"><code>graphStats()</code></a> is a function to extract some of the statists of a graph and make them into a nice string.</p>
<p><code>coCites</code> is now a <a href="https://networkx.github.io/documentation/networkx-1.9.1/"><em>networkx</em></a> graph of the co-citation network, with the hashes of the <code>Citations</code> as nodes and the full citations stored  as an attributes. Lets look at one node</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[28]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">coCites</span><span class="o">.</span><span class="n">nodes</span><span class="p">(</span><span class="n">data</span> <span class="o">=</span> <span class="k">True</span><span class="p">)[</span><span class="mi">0</span><span class="p">]</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[28]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>(-8336129469776275451,
 {&apos;count&apos;: 3, &apos;info&apos;: &apos;GEHENIAU J, 1939, CONTRIBUTION THEORIE, P20&apos;})</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>and an edge</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[29]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">coCites</span><span class="o">.</span><span class="n">edges</span><span class="p">(</span><span class="n">data</span> <span class="o">=</span> <span class="k">True</span><span class="p">)[</span><span class="mi">0</span><span class="p">]</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[29]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>(-8336129469776275451, 9015766391572015105, {&apos;weight&apos;: 1})</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>All the graphs <em>metaknowledge</em> use are <em>networkx</em> graphs, a few functions to trim them are implemented in <em>metaknowledge</em>, <a href="#filtering-graphs">here</a> is the example section, but many useful functions are implemented by it. Read the documentation <a href="https://networkx.github.io/documentation/networkx-1.9.1/">here</a> for more information.</p>
<p>The <code>coCiteNetwork()</code> function has many options for filtering and determining the nodes. The default is to use the <code>Citations</code> themselves. If you wanted to make a network of co-citations of journals you would have to make the node type <code>'journal'</code> and remove the non-journals.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[30]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">coCiteJournals</span> <span class="o">=</span> <span class="n">RC</span><span class="o">.</span><span class="n">coCiteNetwork</span><span class="p">(</span><span class="n">nodeType</span> <span class="o">=</span> <span class="s">&#39;journal&#39;</span><span class="p">,</span> <span class="n">dropNonJournals</span> <span class="o">=</span> <span class="k">True</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="n">mk</span><span class="o">.</span><span class="n">graphStats</span><span class="p">(</span><span class="n">coCiteJournals</span><span class="p">))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>The graph has 89 nodes, 1383 edges, 0 isolates, 40 self loops, a density of 0.353166 and a transitivity of 0.640306
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Lets take a look at the graph after a quick spring layout</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[31]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">nx</span><span class="o">.</span><span class="n">draw_spring</span><span class="p">(</span><span class="n">coCiteJournals</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>A bit basic but gives a general idea. If you want to make a much better looking and more informative visualization you could try <a href="https://briatte.github.io/ggnet/">R</a>, <a href="https://gephi.github.io/">gephi</a> or <a href="http://visone.info/">visone</a>. Exporting to them is covered below in <a href="#exporting-graphs"><strong>Exporting graphs</strong></a>.</p>
<h1 id="Making-a-citation-network">Making a citation network<a class="anchor-link" href="#Making-a-citation-network">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>The <a href="{{ site.baseurl }}/docs/RecordCollection#citationNetwork"><code>citationNetwork()</code></a> method is nearly identical to <code>coCiteNetwork()</code> in its parameters. It has one additional keyword argument <code>directed</code> that controls if it produces a directed network. Read <a href="{{ site.baseurl }}/examples/#Making-a-co-citation-network"><strong>Making a co-citation network</strong></a> to learn more about <code>citationNetwork()</code>.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>One small example is still worth providing. If you want to make a network of the citations of years by other years and have the letter <code>'A'</code> in them then you would write:</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[32]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">citationsA</span> <span class="o">=</span> <span class="n">RC</span><span class="o">.</span><span class="n">citationNetwork</span><span class="p">(</span><span class="n">nodeType</span> <span class="o">=</span> <span class="s">&#39;year&#39;</span><span class="p">,</span> <span class="n">keyWords</span> <span class="o">=</span> <span class="p">[</span><span class="s">&#39;A&#39;</span><span class="p">])</span>
<span class="nb">print</span><span class="p">(</span><span class="n">mk</span><span class="o">.</span><span class="n">graphStats</span><span class="p">(</span><span class="n">citationsA</span><span class="p">))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>The graph has 18 nodes, 24 edges, 0 isolates, 1 self loops, a density of 0.0784314 and a transitivity of 0.0344828
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[33]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">nx</span><span class="o">.</span><span class="n">draw_spring</span><span class="p">(</span><span class="n">citationsA</span><span class="p">,</span> <span class="n">with_labels</span> <span class="o">=</span> <span class="k">True</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Making-a-co-author-network">Making a co-author network<a class="anchor-link" href="#Making-a-co-author-network">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>The <a href="{{ site.baseurl }}/docs/RecordCollection#coAuthNetwork"><code>coAuthNetwork()</code></a> function produces the co-authorship network of the RecordCollection as is used as shown</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[34]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">coAuths</span> <span class="o">=</span> <span class="n">RC</span><span class="o">.</span><span class="n">coAuthNetwork</span><span class="p">()</span>
<span class="nb">print</span><span class="p">(</span><span class="n">mk</span><span class="o">.</span><span class="n">graphStats</span><span class="p">(</span><span class="n">coAuths</span><span class="p">))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>The graph has 45 nodes, 46 edges, 9 isolates, 0 self loops, a density of 0.0464646 and a transitivity of 0.822581
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Making-a-one-mode-network">Making a one-mode network<a class="anchor-link" href="#Making-a-one-mode-network">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>In addition to the specialized network generators <em>metaknowledge</em> lets you make a one-mode co-occurence network of any of the WOS tags, with the <a href="{{ site.baseurl }}/docs/RecordCollection#oneModeNetwork">oneModeNetwork()</a> function. For examples the WOS subject tag <code>'WC'</code> can be examined.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[35]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">wcCoOccurs</span> <span class="o">=</span> <span class="n">RC</span><span class="o">.</span><span class="n">oneModeNetwork</span><span class="p">(</span><span class="s">&#39;WC&#39;</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="n">mk</span><span class="o">.</span><span class="n">graphStats</span><span class="p">(</span><span class="n">wcCoOccurs</span><span class="p">))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>The graph has 9 nodes, 3 edges, 3 isolates, 0 self loops, a density of 0.0833333 and a transitivity of 0
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[36]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">nx</span><span class="o">.</span><span class="n">draw_spring</span><span class="p">(</span><span class="n">wcCoOccurs</span><span class="p">,</span> <span class="n">with_labels</span> <span class="o">=</span> <span class="k">True</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
3qizbvLzovAVOU9Vz05qu4c0OTmZHTt2MHToUGva0aNHGTVqFKGhobhcLlq1asXEiRNPK+Oaa65h
6dKljBs3juDgYOLj48nLy8Pj8fD8888TExNDWFgYW7ZsYeHChQDs3bsXl8tFTExMrfUdOHAgGRkZ
vPLKK8TExNC6dWumT5/O3XffDcDIkSNJSkqiV69etG/fHl9fX/7+959itOr2jZ40ifxTIQgwA4il
4gy3P5AMVM7dDFgL/JeKns7hwEynk9vvvbfOfVf5vqysjMmTJxMeHk5UVBQHDx5k9uzZAIwdO5Y7
77yTfv36ERgYSM+ePfnkk08A6Ny5M/Pnz2fIkCFER0cTGhp6xqbcqnUICQnhd7/7Xa3zzZgxg08/
/ZSgoCAGDBjAwIEDq9V98uTJpKamEhISwty5c/H19eWJJ57ghhtuICQkhE8++YS7776bSZMmkZiY
SFBQEL/+9a+tnuw197P8/Gh4SZELLC0tjcWLF/Phhx/asr5Zs2YRERHRoGbo81VWVkZsRATvHT16
1vf6bgduDwwkr6AAb2/vC1E9kYuWwlfkAiopKbE6V1U98/05yVi5kokjR7L1LEa5ygNu9PXlmSVL
9IAF+UVSs7PIBbJ+/XoiIiKIiopiyJAhTV2dC2ZwYiITUlO5sWVLttc/O9upCN4JTz6p4JVfLJ35
ikijqHykYFePh9FuN3dS/ZGC7wALAgLIdjj0SEH5xVP4ikijKS8vJzMzkwVz5vBpdjatTl3LPVhe
zlVdujB60iQSEhJ0jVd+8RS+InJBFBUVcfjwYQBCQ0MJCgpq4hqJXDwUviIiIjZThysRERGbKXxF
RERspvAVERGxmcJXRETEZgpfERERmyl8RUREbKbwFRERsZnCV0RExGYKXxEREZspfEVERGym8BUR
EbGZwldERMRmCl8RERGbKXxFRERspvAVERGxmcJXRETEZgpfERERmyl8RUREbKbwFRERsZnCV0RE
xGYKXxEREZspfEVERGym8BUREbGZwldERMRmCl8RERGbKXxFRERspvAVERGxmcJXRETEZgpfERER
myl8RUREbKbwFRERsZnCV0RExGYKXxEREZspfEVERGym8BUREbGZwldERMRmCl8RERGbKXxFRERs
pvAVERGxmcJXRETEZgpfERERmyl8RUREbKbwFRERsZnCV0RExGYKXxEREZspfEVERGym8BUREbGZ
wldERMRmCl8RERGbKXxFRERspvAVERGxmcJXRETEZgpfERERmyl8RUREbKbwFRERsZnCV0RExGYK
XxEREZspfEVERGym8BUREbGZwldERMRmCl8RERGb/X+DvdojVvkpNAAAAABJRU5ErkJggg==
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Making-a-two-mode-network">Making a two-mode network<a class="anchor-link" href="#Making-a-two-mode-network">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>If you wish to study the relationships between 2 tags you can use the <a href="{{ site.baseurl }}/docs/RecordCollection#twoModeNetwork"><code>twoModeNetwork()</code></a> function which creates a two mode network showing the connections between the tags. For example to look at the connections between titles(<code>'TI'</code>) and subjects (<code>'WC'</code>)</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[37]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">ti_wc</span> <span class="o">=</span> <span class="n">RC</span><span class="o">.</span><span class="n">twoModeNetwork</span><span class="p">(</span><span class="s">&#39;WC&#39;</span><span class="p">,</span> <span class="s">&#39;title&#39;</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="n">mk</span><span class="o">.</span><span class="n">graphStats</span><span class="p">(</span><span class="n">ti_wc</span><span class="p">))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>The graph has 40 nodes, 35 edges, 0 isolates, 0 self loops, a density of 0.0448718 and a transitivity of 0
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>The network is directed by default with the first tag going to the second.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[38]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">mkv</span><span class="o">.</span><span class="n">quickVisual</span><span class="p">(</span><span class="n">ti_wc</span><span class="p">,</span> <span class="n">showLabel</span> <span class="o">=</span> <span class="k">False</span><span class="p">)</span> <span class="c">#default is False as there are usually lots of labels</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><a href="{{ site.baseurl }}/docs/visual#quickVisual"><code>quickVisual()</code></a> makes a graph with the different types of nodes coloured differently and a couple other small visual tweaks from <em>networkx</em>'s <code>draw_spring</code>.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Making-a-multi-mode-network">Making a multi-mode network<a class="anchor-link" href="#Making-a-multi-mode-network">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>For any number of tags the <a href="{{ site.baseurl }}/docs/RecordCollection#nModeNetwork"><code>nModeNetwork()</code></a> function will do the same thing as the <code>oneModeNetwork()</code> but with any number of tags and it will keep track of their types. So to look at the co-occurence of titles <code>'TI'</code>, WOS number <code>'UT'</code> and authors <code>'AU'</code>.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[39]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">tags</span> <span class="o">=</span> <span class="p">[</span><span class="s">&#39;TI&#39;</span><span class="p">,</span> <span class="s">&#39;UT&#39;</span><span class="p">,</span> <span class="s">&#39;AU&#39;</span><span class="p">]</span>
<span class="n">multiModeNet</span> <span class="o">=</span> <span class="n">RC</span><span class="o">.</span><span class="n">nModeNetwork</span><span class="p">(</span><span class="n">tags</span><span class="p">)</span>
<span class="n">mk</span><span class="o">.</span><span class="n">graphStats</span><span class="p">(</span><span class="n">multiModeNet</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[39]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>&apos;The graph has 108 nodes, 163 edges, 0 isolates, 0 self loops, a density of 0.0282105 and a transitivity of 0.443946&apos;</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[40]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">mkv</span><span class="o">.</span><span class="n">quickVisual</span><span class="p">(</span><span class="n">multiModeNet</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
70cnfR+iAAAAAElFTkSuQmCC
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Beware this can very easily produce hairballs</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[41]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">tags</span> <span class="o">=</span> <span class="n">mk</span><span class="o">.</span><span class="n">tagsAndNames</span> <span class="c">#All the tags, twice</span>
<span class="n">sillyMultiModeNet</span> <span class="o">=</span> <span class="n">RC</span><span class="o">.</span><span class="n">nModeNetwork</span><span class="p">(</span><span class="n">tags</span><span class="p">)</span>
<span class="n">mk</span><span class="o">.</span><span class="n">graphStats</span><span class="p">(</span><span class="n">sillyMultiModeNet</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[41]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>&apos;The graph has 1184 nodes, 59573 edges, 0 isolates, 1184 self loops, a density of 0.0850635 and a transitivity of 0.492152&apos;</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[42]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">mkv</span><span class="o">.</span><span class="n">quickVisual</span><span class="p">(</span><span class="n">sillyMultiModeNet</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
f3B39CEcPP8i4djKau6OPsBMGDkDPY/Dm2ML/gnwIeS+XmBWWZFuJh7nfXNS9H++Z4/Rf8j4iV8q
ATU1c7l1q4uJbaYf5ynCwext93jNPvjGZmjMhd8PBcLmpzMw4wzUZ7PjN7Lfzed5ce9eNmzc+P+5
CD0w3McvlYxPOD/3M399zAeECdEFYA3QB9VvV/PKgV+zcOHC8ZfNnj2b+vr6z/ej6oFm+KWHxmdb
uS3rz1AgT7qYJvVKiqpsFe3H21mxYsWnf7MeCq7xSyUg7EK6x557isC/CCd+fdLqbUJl5RmaX3iB
Qq7AaH6UkdwIgx8MGv3IGH6pBGzfvoVs9mngnx/z1SLwC+AmYVfPFu6Of0JV1XoaGgZ46SVn6cfO
pR6pBGzZsokkSWht/S5DQ38mPLQGIfBbgA7CU8opwnnBt4Cnx7+/svII9fXvc/r0ySmHwitO7uqR
SsiePb+ipaWFdDp8ZisWi2QyM6ipmTU+b2jmzCzz5tUxPDwxZmHevK9y4ECb0Rdg+KWSMzQ0NDag
LaiurnZksv4rhl+SIuPNXUmKjOGXpMgYfkmKjOGXpMgYfkmKjOGXpMgYfkmKjOGXpMgYfkmKjOGX
pMgYfkmKjOGXpMgYfkmKjOGXpMgYfkmKjOGXpMgYfkmKjOGXpMgYfkmKjOGXpMgYfkmKjOGXpMgY
fkmKjOGXpMgYfkmKjOGXpMgYfkmKjOGXpMgYfkmKjOGXpMgYfkmKjOGXpMgYfkmKjOGXpMgYfkmK
jOGXpMgYfkmKjOGXpMgYfkmKjOGXpMgYfkmKjOGXpMgYfkmKjOGXpMgYfkmKjOGXpMgYfkmKjOGX
pMgYfkmKjOGXpMgYfkmKjOGXpMgYfkmKjOGXpMgYfkmKjOGXpMgYfkmKjOGXpMgYfkmKzH8AY0n5
Vk8Lr3MAAAAASUVORK5CYII=
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Post-processing-graphs">Post processing graphs<a class="anchor-link" href="#Post-processing-graphs">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>If you wish to apply a well known algorithm or process to a graph <a href="https://networkx.github.io/documentation/networkx-1.9.1/"><em>networkx</em></a> is a good place to look as they do a good job at implementing  them.</p>
<p>One of the features it lacks though is pruning of graphs, <em>metaknowledge</em> has these capabilities. To remove edges outside of some weight range, use <a href="{{ site.baseurl }}/docs/metaknowledge#drop_edges"><code>drop_edges()</code></a>. For example if you wish to remove the self loops, edges with weight less than 2 and weight higher than 10 from <code>coCiteJournals</code>.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[43]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">minWeight</span> <span class="o">=</span> <span class="mi">3</span>
<span class="n">maxWeight</span> <span class="o">=</span> <span class="mi">10</span>
<span class="n">proccessedCoCiteJournals</span> <span class="o">=</span> <span class="n">mk</span><span class="o">.</span><span class="n">drop_edges</span><span class="p">(</span><span class="n">coCiteJournals</span><span class="p">,</span> <span class="n">minWeight</span><span class="p">,</span> <span class="n">maxWeight</span><span class="p">,</span> <span class="n">dropSelfLoops</span> <span class="o">=</span> <span class="k">True</span><span class="p">)</span>
<span class="n">mk</span><span class="o">.</span><span class="n">graphStats</span><span class="p">(</span><span class="n">proccessedCoCiteJournals</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[43]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>&apos;The graph has 89 nodes, 466 edges, 1 isolates, 0 self loops, a density of 0.118999 and a transitivity of 0.213403&apos;</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Then to remove all the isolates, i.e. nodes with degree less than 1, use <a href="{{ site.baseurl }}/docs/metaknowledge#drop_nodesByDegree"><code>drop_nodesByDegree()</code></a></p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[44]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">proccessedCoCiteJournals</span> <span class="o">=</span> <span class="n">mk</span><span class="o">.</span><span class="n">drop_nodesByDegree</span><span class="p">(</span><span class="n">proccessedCoCiteJournals</span><span class="p">,</span> <span class="mi">1</span><span class="p">)</span>
<span class="n">mk</span><span class="o">.</span><span class="n">graphStats</span><span class="p">(</span><span class="n">proccessedCoCiteJournals</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[44]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>&apos;The graph has 88 nodes, 466 edges, 0 isolates, 0 self loops, a density of 0.121735 and a transitivity of 0.213403&apos;</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Now before the processing the graph can be seen <a href="#Making-a-co-citation-network">here</a>. After the processing it looks like</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[45]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">nx</span><span class="o">.</span><span class="n">draw_spring</span><span class="p">(</span><span class="n">proccessedCoCiteJournals</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
pZJPPvkk8/PzWbduXbZt25YrVqzglStX+Oyzz9Lby4t+KpXNGb3KEuRyBduKzF8l85y7d+9my5Yt
7Q4x+ueff/j666/T3d2dCQkJFU4RWZmIQg2VgxDgKoqjBDhAo+Hx48cdkppu+fLl1Ov1VKlUlhHp
zZjNZg4fPpwRERH87rvvOGTIEKpUKhoMBvbp04f16tWjVqtlREQEp06dyv/+97+3HaOwsJCLFy+m
n58fe/XqZRl15+TksF+/fqxXrx7/+ecfLlq0iAEBATx9+jRNJhOXLl1KX19fPv/885b6w2U5mNjr
2OYsl9PPz4+LFi1iTk4O169fT71SaVcZuOXLlt3x5VhWhaRAgCqAdfz8GBcXRycnJyqVSrrYkVXL
RaGgk5MTL168yBo1arBu3bqcMmUKCwoK+PTTT1MikfDatWvMz8+nk5MT27Zty/fee49+fn4cMmQI
//33X/p6etIA23NalyytUVSlq7xtW+t0d8x9fes8Z4BaTaNEQrVUyubh4VbPc5pMJv7444+Mj4+n
0Wjk6NGjy3QifBCx95kXpQptRwhwFcVR85VKgAqFgrVr12anTp04bNgwfvTRR/ziiy+4bdu2cmv6
lofJZOLIkSMpl8vp6enJdevWlfrebDZz9OjRDAsL48WLF3nixAm6urpy4MCBrFOnDiUSCdu1a8e4
uDi6urqydevWXLRo0W1zqllZWXzvvffo4eHBESNG8MqVKzSbzZw3bx6NRiN/+OEHTp8+nQEBAWzY
sCGjo6P522+/VcjB5G6Cd7fRwG+//cYWLVqwXr16HDFihF0j6hIhKc88WFLa744VknQ6ejo7s2HD
hjbX7yWKqjd17tyZgwYNYnh4ONu3b8/8/Hw+//zzjIuLo7+/P0+ePMmjR4+yZs2a9PT0pLe3N7du
3cr8/Hw2adKEKpWKUz/6iFqJhLG4ew3q8kzNK1FUKrO8tt4pc5Yj5zmvXLnCadOmMSQkhA0bNuQX
X3xxT0Oi7gX2Wn3u1tkRlI8Q4CqMI+Yr/fV6enh40GAwMCoqip07d2aPHj3Ypk0bBgUFUalUMiQk
hO3bt+drr73GGTNmcO3atTx69GiZJtwSrl69yo4dO1IikbBBgwYWb2WySIQnTJjAOnXq8Ny5c1y8
eDHDw8OZm5vLtm3bskePHmzRogWdnZ0ZGRnJ+vXrU6fT8amnnuJ3331X6rgXLlxg//79aTQaOXPm
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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Hm, it looks a bit thinner. Using a visualizer will make the difference a bit more noticeable.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Exporting-graphs">Exporting graphs<a class="anchor-link" href="#Exporting-graphs">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Now you have a graph the last step is to write it to disk. <em>networkx</em> has a few ways of doing this, but they tend to be slow. <em>metaknowledge</em> can write an edge list and node attribute file that contain all the information of the graph. The function to do this is called <a href="{{ site.baseurl }}/docs/metaknowledge#write_graph"><code>write_graph()</code></a>. You give it the start of the file name and it makes two labeled files containing the graph.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[46]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">mk</span><span class="o">.</span><span class="n">write_graph</span><span class="p">(</span><span class="n">proccessedCoCiteJournals</span><span class="p">,</span> <span class="s">&quot;FinalJournalCoCites&quot;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>These files are simple CSVs an can be read easily by most systems. If you want to read them back into Python the <a href="{{ site.baseurl }}/docs/metaknowledge#read_graph"><code>read_graph()</code></a> function will do that.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[47]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre> <span class="n">FinalJournalCoCites</span> <span class="o">=</span> <span class="n">mk</span><span class="o">.</span><span class="n">read_graph</span><span class="p">(</span><span class="s">&quot;FinalJournalCoCites_edgeList.csv&quot;</span><span class="p">,</span> <span class="s">&quot;FinalJournalCoCites_nodeAttributes.csv&quot;</span><span class="p">)</span>
<span class="n">mk</span><span class="o">.</span><span class="n">graphStats</span><span class="p">(</span><span class="n">FinalJournalCoCites</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[47]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>&apos;The graph has 88 nodes, 466 edges, 0 isolates, 0 self loops, a density of 0.121735 and a transitivity of 0.213403&apos;</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>This is full example workflow for <em>metaknowledge</em>, the package is flexible and you hopefully will be able to customize it to do what you want (I assume you do not want the Records staring with 'A').</p>

</div>
</div>
</div>
{% include docsFooter.md %}