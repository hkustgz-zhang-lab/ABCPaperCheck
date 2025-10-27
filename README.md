![ABCPaperCheck](https://socialify.git.ci/wjrforcyber/ABCPaperCheck/image?description=1&font=Rokkitt&language=1&name=1&pattern=Circuit%20Board&theme=Dark)

# Research related to ABC
[ABC](https://github.com/berkeley-abc/abc) is a very popular open source Logic Synthesis project, some research implemented in ABC or related to ABC is recorded here.

This repo also helps people who want to read ABC code properly, research paper is a good start before accessing plain code.

Most of the paper referenced here can be found at Alan Mishchenko's [publication page](https://people.eecs.berkeley.edu/~alanmi/publications/).

Another [EPFL Isils group](https://github.com/lsils) also has very high quality synthesis research, feel free to add anything interesting to the list.

## Unit Test
[TestABC](https://github.com/wjrforcyber/TestABC) is a repository that I sometimes write unit tests for ABC. The credit goes to [@QuantamHD](https://github.com/QuantamHD) for adding the original Google test module and also verification in the github workflow, however, few people add tests to it after that. Writing unit tests can help verify the interface works as expected, it is also a good way to decompose and understand how ABC works under the hood, I start to record some unit tests these days, but I can't make sure I could verify all of them since there are too many. It's probably going to be task-driven like. If you are interested, feel free to add your tests and description of the interfaces in the [README.md](https://github.com/wjrforcyber/TestABC/blob/main/README.md).

## General introduction
- [ABC: An academic industrial-strength verification tool](https://people.eecs.berkeley.edu/~alanmi/publications/2010/cav10_abc.pdf)
<br/>This introduction is a bit old but contains history of all Berkeley's tools and how ABC is started, it is written by Prof Robert Brayton.

- [Quick Look under the Hood of ABC](https://people.eecs.berkeley.edu/~alanmi/abc/programming.pdf)
<br/>A brief but important manual helps understand basic network types and structures in ABC.


## Command and Research Related


<details open>
  <summary>
    <h3>
      Structure & algorithm
    </h3>
  </summary>

Some structure concept such as K-feasible cuts, priority cuts, MFFC in ABC can be found in following research paper.

- [CUDD package](https://web.mit.edu/sage/export/tmp/y/usr/share/doc/polybori/cudd/cuddIntro.html)
<br/>A manual helps get familiar with CUDD package.

- Multi-valued Decision Diagram (MDDs) [Algorithms for discrete function manipulation](https://ieeexplore.ieee.org/document/129849)

- [EXTRA library](https://people.eecs.berkeley.edu/~alanmi/research/extra/)
<br/>Should be used together with CUDD package.

- [Liberty Reference Manual](https://people.eecs.berkeley.edu/~alanmi/publications/other/liberty07_03.pdf), there's probably a new version though, if anyone has a legal reference link, please update.  

- [Priority Cuts Definition](https://people.eecs.berkeley.edu/~alanmi/publications/2007/iccad07_map.pdf)
<br/>Priority cuts are cuts with cost function.

- [Factor Cuts Definition](https://people.eecs.berkeley.edu/~alanmi/publications/2006/iccad06_cut.pdf)
<br/>There are two ways of generating cuts, [top-down or bottom-up](https://infoscience.epfl.ch/entities/publication/d9ae3daa-9ee9-4902-892d-ba7b3f241bfb). 

- [Cut Ranking and Pruning: Enabling A General And Efficient FPGA Mapping Solution](https://dl.acm.org/doi/pdf/10.1145/296399.296425)

- [Fast Heuristic Minimization of Exclusive-Sums-of-Products](https://people.eecs.berkeley.edu/~alanmi/publications/2001/rm01_heu.pdf)
<br>ESOP minimizer EXORCISM-4, compared with early EXMIN2/MINT/EXORCISM-2/EXORCISM–3.

- ISOP(Irredundant Sum-of-product computation)
<br>Which is always computed by Minato-Morreale Algorithm, there is one Pseudo code in the [appendix part](https://cecs.uci.edu/~papers/compendium94-03/papers/1998/iccad98/pdffiles/02b_2.pdf), the truth table library in [Kitty](https://github.com/msoeken/kitty/blob/master/include/kitty/isop.hpp) also has an implementation.
<br>Note BDD package seems to have internal interface. (Reference needed).


</details>


### IO & Util Group

`aigaug`
- [Verilog-to-PyG – A Framework for Graph Learning and Augmentation on RTL Designs](https://people.eecs.berkeley.edu/~alanmi/publications/2023/iccad23_ml.pdf)
- Logic-level augmentation.
- Relevant [repository](https://github.com/Yu-Maryland/Verilog-to-PyG).

`&get` & `&put`
- ABC has ABC space and ABC9 space, example of using them interchangeably:
<br> `read_aiger i10.aig; strash; &get; &b; &st; &put; rewrite; refactor; ps`
<br> `&r i10.aig; &st; &if -g; &put; balance; rewrite; ps`
<br> `read_aiger i10.aig; strash; &get; &if -g; &ps`

`read_aiger`
- [Local Two-Level And-Inverter Graph Minimization without Blowup](https://fmv.jku.at/papers/BrummayerBiere-MEMICS06.pdf)
<br>This one is referenced in ABC when constructing AIG.
- [AIGER 1.9 AND Beyond](https://fmv.jku.at/papers/BiereHeljankoWieringa-FMV-TR-11-2.pdf)
- [The AIGER And-Inverter Graph (AIG) Format Version 20071012](https://fmv.jku.at/papers/Biere-FMV-TR-07-1.pdf)
<br>This version is much more detailed than the latest one and illustrates the original AIG format and how to parse it. If you are working on a parser, read this carefully, I recommend reading the [aiger parser in lorina](https://github.com/hriener/lorina/blob/master/include/lorina/aiger.hpp), which is implemented in regular expression, in ABC, this is done by hard-core char by char shifting.
<br>Prof Armin Biere's [repo](https://github.com/arminbiere/aiger) would help you do the transformation between aig and other format.

`read_bench` 
- Read a [bench format file](https://sportlab.usc.edu/~msabrishami/benchmark-project/bench.html)

`read_blif`
- [Berkeley Logic Interchange Format(BLIF)](https://course.ece.cmu.edu/~ee760/760docs/blif.pdf)
- [BLIF-MV](https://people.eecs.berkeley.edu/~alanmi/publications/other/blifmv.pdf)
<br>BLIF-MV format is the extended BLIF format.

`read_pla`
<br>PLA format is used as the input file format for Espresso, could find the manual [here](https://people.eecs.berkeley.edu/~alanmi/research/espresso/espresso_5.html).

`read_genlib` & `print_genlib`
- genlib format is [SIS genlib format](https://workcraft.org/_media/help/sis_genlib.pdf)
<br>*Note this is not an official source, it would be appreciated if anyone could provide an official source.

`read_super`
- Concepts of supergates can be found in [Reference0](https://people.eecs.berkeley.edu/~alanmi/publications/2005/tech05_map.pdf) and [Reference1](https://people.eecs.berkeley.edu/~alanmi/publications/2005/tcad05_map.pdf).
  
`super`
- In ABC this command for constructing supergates only accepts a library in genlib format, if you are using a standard cell library, dump a genlib first.

`testnpn`
- [Fast Boolean Matching Based on NPN Classification](https://people.eecs.berkeley.edu/~alanmi/publications/2013/icfpt13_npn.pdf)
- [Fast Adjustable NPN Classification Using Generalized Symmetries](https://people.eecs.berkeley.edu/~alanmi/publications/2019/trets19_npn.pdf)

`double`
- *double* can be used to increase the size of the current aig network, and functionally speaking, you could generate larger case more realistic than MtM benchmark. - [Reference](https://people.eecs.berkeley.edu/~alanmi/publications/2018/iccad18_rwr.pdf)

`&cec`
- [Parallel Combinational Equivalence Checking](https://people.eecs.berkeley.edu/~alanmi/publications/2019/tcad19_cec.pdf)
<br>Note that exact `-P` and `-S` switch cannot be found here, if anyone has found the exact implementation in the paper, please update. 

`write_edgelist`
- [Verilog-to-PyG – A Framework for Graph Learning and Augmentation on RTL Designs](https://people.eecs.berkeley.edu/~alanmi/publications/2023/iccad23_ml.pdf)
- Graph Extraction.

`write_bench`
- This command by default write out the LUT network, if you prefer the traditional gate representation, turn on `-l`.

### Optimization Group

`strash`
<br>Structural hashing
- One-level strashing: Make sure nodes have different fanins(up to permutation).
- [Two-level strashing](https://fmv.jku.at/papers/BrummayerBiere-MEMICS06.pdf)

`bdd`
<br>Binary decision diagram.
<br>*Note that Reduced Ordered Binary Decision Diagram(ROBDD) is canonical but even with structure hashing, AIG is not canonical, this is simple but important.

`bidec`
<br>Bi-decomposition.
<br>Reference: [An Algorithm for Bi-Decomposition of Logic Functions](https://people.eecs.berkeley.edu/~alanmi/publications/2001/dac01.pdf) (Compared to SIS, better delay result achieved.)

`dsd`
- [The Disjunctive Decomposition of Logic Functions](https://dl.acm.org/doi/pdf/10.5555/266388.266429)
<br> This command implements all the 4 cases in the paper above.
- Other Disjoint Support Decomposition reference:
  - [Minato-DeMicheli](https://dl.acm.org/doi/pdf/10.1145/288548.288586)
  - [Sasao-Matsuura](http://www.lsi-cad.com/sasao/Papers/files/IWLS1998.pdf)
  - [An approach to disjoint-support decomposition of logic functions](https://people.eecs.berkeley.edu/~alanmi/publications/2001/tech01_dsd.pdf)
  <br>This implementation should be in [EXTRA](https://people.eecs.berkeley.edu/~alanmi/research/extra/) library.

`dsec`
<br>Sequential Equivalence Checking.
- [Scalable and Scalably-Verifiable Sequential Synthesis](https://people.eecs.berkeley.edu/~brayton/publications/2008/dac08_vss.pdf)

`eliminate`
- [Reference](https://people.eecs.berkeley.edu/~alanmi/publications/2006/iwls06_sls.pdf): *"For example, the operation “eliminate” collapses a node into its fanouts if the worth of a node computed using this metric did not exceed a specified threshold."*("this metric" stands for FFLC.)

`&fx`
- Fast extract from [The Testability-Preserving Concurrent Decomposition and Factorization of Boolean Expressions](https://ieeexplore.ieee.org/document/137523)

`ftune`
- [FlowTune: End-to-end Automatic Logic Optimization Exploration via Domain-specific Multi-armed Bandit](https://arxiv.org/abs/2202.07721)
<br>Note that this command **is not in the original ABC**, the detail of the implementation is [here](https://github.com/Yu-Maryland/FlowTune).

`fraig`
- [FRAIGs: A Unifying Representation for Logic Synthesis and Verification](https://people.eecs.berkeley.edu/~alanmi/publications/2005/tech05_fraigs.pdf)
<br>Construct aig and make sure it's semi-canonical, the concept **semi-canonical** can be compared with ROBDD, which is totally canonical.
<br>*Note that the MVSIS link in the paper is no longer available, unofficial source code could be retrieved from the **Traditional Logic synthesis tools** part below.

`&iso`
- [A Semi-Canonical Form for Sequential AIGs](https://people.eecs.berkeley.edu/~alanmi/publications/2013/date13_iso.pdf)

`orchestrate`
- [DAG-aware Synthesis Orchestration](https://arxiv.org/pdf/2310.07846)
- Greedy local optimization and domain specific optimization with orchestration of `rewrite`/`refactor`/`resub`.

`profile`
- It profiles the gate structure in network, uses reverse engineer, helps when using transparent-boxing strategy and optimizing with don't care.
- `-a` HA and FA: [Structural reverse engineering of arithmetic circuits](https://people.eecs.berkeley.edu/~alanmi/publications/2017/tech17_arith.pdf)

`rewrite/refactor/balance`
- [DAG-Aware AIG Rewriting A Fresh Look at Combinational Logic Synthesis](https://people.eecs.berkeley.edu/~alanmi/publications/2006/dac06_rwr.pdf)
<br>*Note that based on this [thread](https://github.com/YosysHQ/yosys/issues/4039), you should consider using `drw/drf`.
- For `balance`, check the [original paper](https://www.cs.upc.edu/~jordicf/gavina/BIB/files/tcad03_bidec.pdf) about bi-decomposition.
- Note that in ABC, `balance` command have `-d` and `-s` option but implemented improperly which leads to same result, in mockturtle, the same algorithm skips these two options.

`resub`
- [Scalable Logic Synthesis using a Simple Circuit Structure](https://people.eecs.berkeley.edu/~alanmi/publications/2006/iwls06_sls.pdf)
<br>*Note that this resub is technology-independent, there is technology-dependent resub in [reference](https://people.eecs.berkeley.edu/~alanmi/publications/2005/tcad05_s&s.pdf), they have similar idea.

`resub_unate`
- Fast resub based on detecting unate divisors
- [A Simulation-Guided Paradigm for Logic Synthesis and Verification](https://people.eecs.berkeley.edu/~alanmi/publications/2021/tcad21_sim.pdf)

`resub_core`
- Generic high-effort resub engine based on support selection	
- [Efficient Computation of ECO Patch Functions](https://people.eecs.berkeley.edu/~alanmi/publications/2018/dac18_eco.pdf)

`twoexact`
- SAT-based exact synthesis with side-divisors
- [SAT Based Exact Synthesis using DAG Topology Families](https://people.eecs.berkeley.edu/~alanmi/publications/2018/dac18_topo.pdf)
<br>*Note: The above three commands with commands such as `runeco` and `&genrel` can be found in [this repo](https://github.com/alanminko/resub).

`&reshape`
- [Control Logic Restructuring for Area Optimization](https://people.eecs.berkeley.edu/~alanmi/publications/2022/iwls22_reshape.pdf)
<br>*Note that although this command is already in ABC, no real implementation is available.

`rr`
- [Scalable Logic Synthesis using a Simple Circuit Structure](https://people.eecs.berkeley.edu/~alanmi/publications/2006/iwls06_sls.pdf)
<br>The concept of redundancy removal can be found here. The original redundancy removal could still be found in ABC source code but is not registered in the tool, so you can't use it directly, it is marked as absolete.
<br>*Note: *"... Therefore, don’t-care-based two-level minimization performed in ... using ESPRESSO is not needed for AIG."*

`runeco`
- [Efficient Computation of ECO Patch Functions](https://people.eecs.berkeley.edu/~alanmi/publications/2018/dac18_eco.pdf)

`satclp`
- [Progressive Generation of Canonical Irredundant Sums of Products Using a SAT Solver](https://people.eecs.berkeley.edu/~alanmi/publications/2017/book17_satclp.pdf)

`&satlut`
- [SAT-Based Area Recovery in Structural Technology Mapping](https://people.eecs.berkeley.edu/~alanmi/publications/2018/aspdac18_satlut.pdf)

`&transduction`
- [Randomized Transduction for High-Effort Logic Synthesis](https://people.eecs.berkeley.edu/~alanmi/publications/2024/iwls24_transd.pdf)

`lutmin`
- [Encoding of Boolean functions and its application to LUT cascade synthesis](https://people.eecs.berkeley.edu/~alanmi/publications/2002/iwls02_enc.pdf)
<br>The paper itself does not mention ABC but in this [paper](https://people.eecs.berkeley.edu/~alanmi/publications/2023/iwls23_lut.pdf), reference links `lutmin` here.

`lutpack`
- [Fast Boolean Matching for LUT Structures](https://people.eecs.berkeley.edu/~alanmi/publications/2007/tech07_lpk.pdf)
- [Boolean Factoring and Decomposition of Logic Networks](https://people.eecs.berkeley.edu/~alanmi/publications/2008/iccad08_lp.pdf)

`dchoice`
<br> *Note: *"The command dchoice uses various methods for rewriting the AIG to minimize the number of AIG nodes while not increasing the number of its levels. In particular, dchoice strives for smaller delay by “balancing”, which decreases the number of AIG levels by decomposing “wide-input” AND gates in a balanced way."* - [Reference](https://people.eecs.berkeley.edu/~alanmi/publications/2010/fpga10_speedup.pdf)

`indcut`
- [Cut-Based Inductive Invariant Computation](https://people.eecs.berkeley.edu/~alanmi/publications/2008/iwls08_ind.pdf)
<br>You will see why one-hotness is collected in section 3.2, this technique is also used in command such as `mfs`.

`if -S`
- [Mapping into LUT Structures](https://people.eecs.berkeley.edu/~alanmi/publications/2012/date12_lut.pdf)


`if -g` 
- [Delay Optimization Using SOP Balancing](https://people.eecs.berkeley.edu/~alanmi/publications/2011/iccad11_sop.pdf)
<br>*Openroad flow use SOP balance in their [script](https://github.com/The-OpenROAD-Project/OpenROAD-flow-scripts/blob/master/flow/scripts/abc_speed.script) (Update 2024.1.2).
<br>Optimize some aig structure rw/rf/b can't optimize.

`if -y`
- [Lazy Man’s Logic Synthesis](https://people.eecs.berkeley.edu/~alanmi/publications/2012/iccad12_lms.pdf)
<br>Frequency based method to collect better pattern from design. Can even deal with patterns SOP-balance can not break.

`if -u` 
- [Busy Man’s Synthesis: Combinational Delay Optimization With SAT](https://people.eecs.berkeley.edu/~alanmi/publications/2017/date17_bms.pdf)


### Mapper Group
`map`
<br>There are tons of ideas and tricks inside the mapper, this list will be extended.
- [Reducing Structural Bias in Technology Mapping](https://people.eecs.berkeley.edu/~alanmi/publications/2005/iccad05_map.pdf)
- [Technology Mapping with Boolean Matching, Supergates and Choices](https://people.eecs.berkeley.edu/~alanmi/publications/2005/tech05_map.pdf)
- [Logic effort: Designing for speed on the back of an Envelope](https://www.ece.ucdavis.edu/~vojin/CLASSES/EPFL/Papers/LE-orig-paper.pdf)
<br>Core theory, logic effort.
- [Gain-Based Technology Mapping for Discrete-Size Cell Libraries](https://ieeexplore.ieee.org/document/1219085)
<br>Some gain-based method reference.
<br>This reference is closely related to standard cell library mapping, which has discrete-size in each cell class (which means assumption of continuously sizeable cells does not hold).
- Why delay estimation is logarithmic? [High-Level Delay Estimation for Technology-Independent logic Equations](https://ieeexplore.ieee.org/document/129876/)


`if`
- [Combinational and Sequential Mapping with Priority Cuts](https://people.eecs.berkeley.edu/~alanmi/publications/2007/iccad07_map.pdf)

`&sif`
- [Mapping and Retiming Revisited](https://people.eecs.berkeley.edu/~alanmi/publications/2023/iwls23_m&r.pdf)

`smap` & `sfpga`
- [Integrating Logic Synthesis, Technology Mapping, and Retiming](https://people.eecs.berkeley.edu/~alanmi/publications/2006/tech06_int.pdf)

`atmap`
- A Design of Compressor Trees for LLM Module (IWLS 2025)

#### Other reference
- Recommend this [slide](http://cc.ee.ntu.edu.tw/~jhjiang/instruction/courses/fall14-lsv/lec08_2p.pdf) about technology mapping by Prof Jie-Hong Roland Jiang.
- [FlowMap: An Optimal Technology Mapping Algorithm for Delay Optimization
in Lookup-Table Based FPGA Designs](https://limsk.ece.gatech.edu/course/ece6133/papers/flowmap.pdf)
<br>FlowMap
- [Chortle: A Technology Mapping Program for Lookup Table-Based Field Programmable Gate Arrays](https://dl.acm.org/doi/pdf/10.1145/123186.123418)
<br>Chortle
- [Chortle-crf Fast Technology Table-Based Mapping for FPGAs](https://www.ece.iastate.edu/~zambreno/classes/cpre583/documents/FraRos91A.pdf)
<br>Chortle-crf
- [DAGON: Technology Binding and Local Optimization by DAG Matching](https://dl.acm.org/doi/pdf/10.1145/62882.62957)
<br>The well known DAGON, you could probably see this in any reference(especially lecture slides/research paper etc.) online. Based on treeifying and dynamic programming.
- [Delay-Optimal Technology Mapping by DAG Covering](https://dl.acm.org/doi/pdf/10.1145/277044.277142)
<br>DAG mapper
<br>*Note: Faster than tree covering method in DAGON.
- [Logic Decomposition during Technology Mapping](https://dl.acm.org/doi/pdf/10.5555/224841.225050)
<br>Graph mapper
<br>*Note: *"Using supergates and choices, the mapper outperforms both **Graph Map** and **DAG mapper** in delay and area and has a significantly shorter run-time."* - [Reference](https://people.eecs.berkeley.edu/~alanmi/publications/2005/iccad05_map.pdf).


### Post-Mappinng Group
`speedup`
- [Global Delay Optimization using Structural Choices](https://people.eecs.berkeley.edu/~alanmi/publications/2009/tech09_speed.pdf)
<br>*Note: ABC LUT library format also has examples in this paper. Since all optimization is on AIG as `strash` is performed after time tracing and critical node marking, so change these two part will help to apply the algorithm after standard cell mapping.

`mfs` & `mfs2` & `&mfs`
- [Scalable Don’t-Care-Based Logic Optimization and Resynthesis](https://people.eecs.berkeley.edu/~alanmi/publications/2011/trets11_mfs.pdf)
<br>Re-sub based resynthesis + don't care based resynthesis
- Recommend using `&mfs` which is believed to be the newest and best version in ABC. (See note 5 on Page 12 of [Reference](https://people.eecs.berkeley.edu/~alanmi/publications/2021/tcad21_sim.pdf).)

`mfs3`
- [Versatile SAT-based Remapping for Standard Cells](https://people.eecs.berkeley.edu/~alanmi/publications/2016/iwls16_mfs3.pdf)
<br> Experiment is performed after `amap` and `&nf -R 1000`.
<br> *Note: `mfs` & `mfs2` are for **LUT-based FPGAs** while `mfs3` is for **standard cells**.
<br> *Gain-based [approach](https://www.ece.ucdavis.edu/~vojin/CLASSES/EPFL/Papers/LE-orig-paper.pdf) deals with delay information.

#### NPN
- [Classifying n-Input Boolean Functions](https://iie.fing.edu.uy/investigacion/grupos/microele//iberchip/pdf/75.pdf)
<br> Very clear illustration of P/NPN class and examples are shown.

### Verification Group

#### Property Checking & SEC (Sequential Equivalence Checking)

`pdr`
- [(2011) Efficient Implementation of Property Directed Reachability](https://people.eecs.berkeley.edu/~alanmi/publications/2011/fmcad11_pdr.pdf)
<br>Implements the Property Directed Reachability (PDR/IC3) algorithm, optimized for AIGs, for model checking safety properties.

`bmc` / `&bmc` / `&bmcs` / `bmc2` / `bmc3`
- [(1999) Symbolic Model Checking without BDDs](https://fmv.jku.at/papers/BiereCimattiClarkeZhu-TACAS99.pdf)
<br>Performs Bounded Model Checking (BMC). ABC offers multiple implementations (`bmc`, `&bmc`, `&bmcs`, `bmc2`, `bmc3`) with varying features like static/dynamic unrolling, parallel solver support, etc.

`ind`
- [(2000) Checking Safety Properties Using Induction and a SAT-Solver](https://link.springer.com/chapter/10.1007/3-540-40922-X_8)
<br>Performs K-step Induction to verify safety properties using a SAT solver.

`int`
- [(2003) Interpolation and SAT-based Model Checking](https://link.springer.com/chapter/10.1007/978-3-540-45069-6_1)
<br>Uses SAT-based interpolation to perform model checking.

`dprove` 
- [Enhancing and Integrating Model Checking Engines](https://www.slideserve.com/jamesengel/enhancing-and-integrating-model-checking-engines-powerpoint-ppt-presentation)
<br>Performs Sequential Equivalence Checking (SEC) on a sequential miter, combining techniques like abstraction refinement, speculative reduction.

`reach` / `&reachm` / `&reachn` / `&reachp` / `&reachy`
- [(1992) Symbolic model checking: 10^20 states and beyond](https://dl.acm.org/doi/10.1016/0890-5401%2892%2990017-A) (Foundational paper on BDD reachability)
<br>Performs BDD-based reachability analysis for model checking. ABC provides multiple implementations (`reach`, `&reachm`, `&reachn`, `&reachp`, `&reachy`) using different BDD techniques and optimizations. 

`tempor`
- [(2009) Enhanced Verification by Temporal Decomposition](https://ieeexplore.ieee.org/document/5351146/)
<br>Leverages temporal decomposition techniques to improve efficiency in sequential verification.

`indcut`
- [(2008) Cut-Based Inductive Invariant Computation](https://people.eecs.berkeley.edu/~alanmi/publications/2008/iwls08_ind.pdf)
<br>Uses cut-based methods to compute inductive invariants for model checking.

`l2s`
- [(2002) Liveness Checking as Safety Checking](https://fmv.jku.at/papers/BiereArthoSchuppan-FMICS02.pdf) (Describes the underlying liveness-to-safety transformation) 
<br>Performs a liveness-to-safety transformation, converting the check of a liveness property into a safety property check.

`kcs`
- [(2012) A liveness checking algorithm that counts](https://fmv.jku.at/papers/BiereArthoSchuppan-FMICS02.pdf)
<br>Implements Claessen-Sorensson's k-Liveness algorithm for checking liveness properties.

#### LEC & Miter Solving & SAT Solving (Combinational Equivalence & SAT)

`cec` / `&cec`
- [(2006) Improvements to combinational equivalence checking](https://people.eecs.berkeley.edu/~alanmi/publications/2006/iccad06_cec.pdf) (Discusses techniques used in CEC)
<br>Performs Combinational Equivalence Checking (CEC), comparing two combinational circuits or a combinational miter.

`&acec`
- [Equivalence Checking using Gr ̈obner Bases](https://ics.jku.at/files/2016FMCAD_ACEC.pdf)
<br>Performs Combinational Equivalence Checking specialized for arithmetic circuits (e.g., multipliers).

`iprove`
- [(2006) Improvements to combinational equivalence checking](https://people.eecs.berkeley.edu/~alanmi/publications/2006/iccad06_cec.pdf)
<br>A newer engine for Combinational Equivalence Checking (CEC), integrating multiple techniques (rewriting, Fraiging, BDDs, SAT).

`fraig` / `&fraig` / `dfraig` / `ifraig`
- [(2003) FRAIGs: A Unifying Representation for Logic Synthesis and Verification](https://people.eecs.berkeley.edu/~alanmi/publications/2005/tech05_fraigs.pdf)
<br>Performs combinational SAT sweeping to build Functionally Reduced And-Inverter Graphs (FRAIGs), a core technique for CEC.

`sat` / `&sat`
- [Chaff: Engineering an Efficient SAT Solver](https://www.princeton.edu/~chaff/publication/DAC2001v56.pdf) (Pioneering work in modern SAT solvers often used as baseline/inspiration)
<br>Performs SAT solving to check the satisfiability of combinational circuit outputs, commonly used for miter solving. Often integrates solvers like MiniSat internally.

`dsat` / `&dsat`
- [An Extensible SAT-solver (MiniSat)](https://lara.epfl.ch/w/_media/projects:minisat-anextensiblesatsolver.pdf) (Describes MiniSat, often used by `dsat`)
<br>Solves combinational miter SAT problems, often using an embedded MiniSat solver.

## Delay target optimization
- [Enabling Exact Delay Synthesis](https://people.eecs.berkeley.edu/~alanmi/publications/2017/iccad17_eds.pdf)
<br> Personally really recommend this paper which combines timing information with supergates and optimizes searching using P classes with timing pattern.

## Area target optimization



## Traditional Logic synthesis tools
A brief historical view and corresponding introduction of UCB's synthesis and verification tool set:

<img src="images/image.png" width="900">

- [Old Logic synthesis tools](https://jackhack96.github.io/logic-synthesis/mvsis.html)
<br>Espresso, SIS, MVSIS are here.
<br>*Note: Some algorithm in ABC is directly from SIS and MVSIS.

- MIS [MIS: A Multiple-Level Logic Optimization System](https://ieeexplore.ieee.org/document/1270347)
- SIS [SIS: A System for Sequential Circuit Synthesis](https://www2.eecs.berkeley.edu/Pubs/TechRpts/1992/ERL-92-41.pdf)
- VIS(Verification Interacting with Synthesis)[VIS : A System for Verification and Synthesis](https://www.cs.columbia.edu/~sedwards/papers/brayton1996vis.pdf)
- MVSIS [MVSIS 2.0 Programmer’s Manual](https://ptolemy.berkeley.edu/projects/embedded/mvsis/doc/mvsis_20_prog.pdf)
<details>
  <summary>
    <h2>
      Benchmarks
    </h2>
  </summary>
  Here are some famous benchmarks from research/paper above.

- [ESPRESSO benchmark](https://ptolemy.berkeley.edu/projects/embedded/pubs/downloads/espresso/index.htm)
- [IWLS 2022 Benchmarks](https://github.com/alanminko/iwls2022-ls-contest)
- [IWLS 2005 Benchmarks](https://iwls.org/iwls2005/benchmarks.html)
- [IWLS 2024 Benchmarks](https://github.com/alanminko/iwls2024-ls-contest)
- [EPFL combinational benchmark suite](https://github.com/lsils/benchmarks)
<br>There's also a [paper](https://core.ac.uk/download/pdf/148012141.pdf) related to the benchmark.
<br>*Note that case `hyp` is quite big and skip it if necessary.
- Official AIG benchmarks can be found at [here](https://fmv.jku.at/aiger/).
- [ISCAS](https://web.eecs.umich.edu/~jhayes/iscas.restore/)
- [ITC99](https://github.com/cad-polito-it/I99T)
- [MCNC](https://s2.smu.edu/~manikas/Benchmarks/MCNC_Benchmark_Netlists.html)
- [ISPD’02 IBM Mixed-Size Placement Benchmarks](http://vlsicad.eecs.umich.edu/BK/ISPD02bench/)
- [ISPD’98 Circuit Benchmark Suite](https://cseweb.ucsd.edu/~kastner/labyrinth_vault/benchmarks/index.html) - [Reference](https://dl.acm.org/doi/pdf/10.1145/274535.274546)
- [ISPD04 IBM Standard Cell Benchmarks with Pads](http://vlsicad.eecs.umich.edu/BK/Slots/cache/www.public.iastate.edu/~nataraj/ISPD04_Bench.html)
- [MPC Benchmark](https://github.com/lsils/date2020_experiments/tree/master/MPC_benchmarks)
- [Crypto Benchmark](https://github.com/lsils/date2020_experiments/tree/master/crypto_benchmarks)
</details>




## Other repo
[Yosys](https://github.com/YosysHQ/yosys) and [OpenRoad-flow-scripts](https://github.com/The-OpenROAD-Project/OpenROAD-flow-scripts) are good place to find out discussion about ABC since original ABC repo's issues are not very active.


<details>
  <summary>
    <h3>
      SAT solver
    </h3>
  </summary>

This [repo](https://www.cs.cmu.edu/~mheule/15816-f21/slides/practice.pdf) from CMU can give you a brief introduction on the DIMACS format and how to use SAT solver as an interface.

I was trying to maintain a collection list of SAT solvers, but I have found that [PySAT](https://github.com/pysathq/pysat) seems to contain all the well-known SAT solvers. 

There's a detailed [introduction](https://people.eecs.berkeley.edu/~alanmi/courses/2007_290N/papers/intro_een_sat03.pdf) on MiniSAT.

</details>

## Performance
- Yosys+ABC9 in FPGA is catching up with industry level performance. - [Reference](https://people.eecs.berkeley.edu/~alanmi/publications/2023/date23_gap.pdf)

- IWLS 2024: Yosys+ABC(Lazy Man Based): [Insights from Basilisk: Are Open-Source EDA Tools Ready for a Multi-Million-Gate, Linux-Booting RV64 SoC Design?](https://arxiv.org/pdf/2405.04257)


## TODO
Some of the implementation was originally been written into the traditional tools such as MVSIS or SIS.
<br>It's better to check if ABC contains the following.
- *“S&S-based and BDD-based resubstitution algorithms were implemented in the resynthesis package used to improve the quality of standard-cell technology mapping in MVSIS”* - [Reference](https://people.eecs.berkeley.edu/~alanmi/publications/2005/tcad05_s&s.pdf)
