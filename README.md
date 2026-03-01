# Thesis
-   Title: **Development of a self-parameterizing Genetic Algorithm:**
    A Case Study on High School Timetabling

-   Degree: Mobile and Distributed Computing
-   Advisor: Dr. Eric Veith


# Table of Contents

<!-- Chapter 1 ------------------------------------------------------------- -->
## 1. Introduction
-   ✅ introduction into timetabling, GAs and my thesis

### 1.1. Motivation (Status Quo)
<!-- Describe Status Quo -->
-   ✅ short introduction into timetabling and its NP-completeness (why
    deterministic algorithms cannot be used for solving such problems)

-   refer to my research paper
    -   ✅ GAs are (somewhat) used in educational timetabling,
        but only *rarely* in high-school timetabling

    -   ✅ regarding university timetabling, the ITC (2007 or whatever) problem
        instances are commonly used to compare algorithms/solvers,
        among the *high-school timetabling* algorithms no common problem
        instances have been used (although available -> XHSTT)

    -   ✅ these (few) known algorithms don't:
        -   publish their implementation (for reproducing the results)
        -   use standardized problem instances which would allow for comparison
        -   go into detail about runtime etc.

    -   ✅ as highlighted in my research paper, adaptive evolutionary
        techniques are rarely implemented, despite their promise to
        improve the search process

<!-- Work out a research gap from the status quo -->
> ✅ **Research Gap:** The published GAs for high-school timetabling problems
> cannot be compared as they lack common problem instances for comparison and
> their results cannot be reproduced because the code is not openly accessible.


### 1.2. Contributions and Constraints
<!-- Describe my approach -->
-   approach
    -   ✅ develop two GAs (one with direct, the other with indirect encoding)
        which solve some of the XHSTT instances (hdtt4 and 5)
    -   ✅ develop self-parameterization methods for those algorithms
    -   ✅ analyze the algorithms and compare how the self-parameterization
        changes their behavior by running each algorithm multiple times with
        different configurations (input parameters)

-   contributions
    -   ✅ baseline GA for high-school timetabling problems
    -   ✅ implementation of advanced GA techniques (self-parameterization)
    -   ✅ using a common ground for comparison (XHSTT instances; hdtt4/5)
    -   ✅ make algorithm implementation available (open-source) to allow
        reproducability and simplify future research

-   constraints
    -   ✅ focus on *pure* GAs (no hybrid etc.)
    -   ✅ focus on the XHSTT instances hdtt4 (and 5)
        -   smaller set of constraints
        -   only hard constraints

<!-- Formulate the research hypothesis and/or a research question -->
-   ✅ research hypothesis
    -   adaptive evolutionary techniques in form of self-parameterization
        can have a positive impact on the GA's runtime and/or success rate
        (in solving the problem at hand).

### 1.3. Outline
-   ✅ describe the organization/chapters of this thesis


<!-- Chapter 2 ------------------------------------------------------------- -->
## 2. Foundations and Related Work
<!-- Timetabling -->
-   ✅ timetabling
    -   ✅ mention how timetabling problems differ (high school vs university)
    -   🚧 related work: the XHSTT "project" (there are one/two papers
        describing the effort of creating a common ground for comparing
        high-school timetabling solvers)
        -   ✅ when adding citations, check those papers and maybe change
            some wording

    -   ✅ describe everything about timetabling and XHSTT that's needed in
        further chapters:
        -   ✅ XHSTT format
        -   ✅ fitness = cost and lower cost is better (best is 0 = problem solved)
        -   ✅ mention, that hdtt4 and hdtt5 provide the resource allocation
            information as part of the problem instance/description.
        -   ✅ XHSTT and its common "wording" must be introduced, especially how
            solutions looks like etc.

<!-- Genetic algorithm -->
-   GAs
    -   ✅ related work: the two algorithms from my research paper, which use
        GAs on high-school timetabling problem
        -   ✅ highlight again, that they don't provide runtime/performance
            details, don't use XHSTT and didn't open-source their
            implementation/code
    -   ✅ describe everything about GAs that's needed in further chapters:
        -   ✅ describe how GAs work
        -   ✅ introduce words (chromosome, individual, etc)
        -   ✅ encoding (genotype and phenotype) <!-- Used in chapter 3 -->
        -   ✅ direct an indirect encoding

    -   ✅ problem: parameter tuning -> self-parameterization

<!-- Methods -->
-   ❌ methods
    =>  ditched, because all of these things have been mentioned previously
        in the text (chapter 1 & 2)

    -   ❌ this work focuses on the general effects of self-parameterization on
        GAs and *not* on developing the most elaborate self-parameterization
        methods
    -   ❌ the developed self-parameterization methods reach from very simple
        and not related to population stats, to more elaborate (continuous and
        not-continuous) adaptations, based on population metrics.
    -   ❌ Mention that Rust is used for implementation, and maybe give a
        reason why
        -   performance
        -   zero-cost abstractions allow for readable code and ergonomic
            modelling of timetabling problems, without a hit in performance


<!-- Chapter 3 ------------------------------------------------------------- -->
## 3. Problem Representation
-   ✅ describe my encodings
    -   ✅ direct (genotype + phenotype)
        -   ✅ add graphics to visualize the encoding with bit vectors
        -   ✅ describe what sub-events are (groups of ones in the bit vec)
        -   ✅ mention, where the inspiration for this encoding, for the
            bitvectors and so on comes from -> bitvec paper

        ->  ✅ mention, that the assign-time-constraint must not be evaluated
        in the direct encoding, because this is ensured by the genetic search
        process (operations)

    -   ✅ indirect (genotype + phenotype)
        -   ✅ add graphics to visualize the heuristic algorithm
        -   ✅ inspired by (I think it was) Than???

        ->  ✅ mention, that the avoid-clashes-constraint must not be evaluated
        in the indirect encoding, because this is ensuredby the heuristic

-   ✅ describe the objective of the algorithms in context of the XHSTT
    instances hdtt4/5

-   ✅ describe the evaluation process


<!-- Chapter 4 ------------------------------------------------------------- -->
## 4. Genetic Algorithm
-   ✅ my GA implements all the "normal"/textbook features of a GA
    -   ✅ describe the generalization of the algorithm implementation by using
        my own GA framework
    -   ✅ *maybe* describe the logging and automation capabilities

    -   ✅ der ganze allgemeine Kram sollte vielleicht in
        "Foundations etc." rein, oder nicht?!?!

-   list and describe all:
    -   selection methods (impl. in the GA framework)
        -   ✅ roulette wheel
        -   ✅ n-tournament
        -   ✅ linear rank

    -   crossover methods (alg/encoding specific)
        -   ✅ uniform
        -   ✅ single point
        -   ✅ multi point
        -   ✅ ordered
        -   ✅ pmx
        -   ✅ trade (direct encoding)

    -   mutation methods (alg/encoding specific)
        -   ❌ randomize (not used anywhere)
        -   ✅ swap
        -   ✅ trade (direct enc)
            -   feedback: describe in more detail (pseudo-code)
                =>  I don't see a need for this as the operation is exactly the
                    same as the n-Trade crossover, which was described in great
                    detail by a illustration
                =>  I modified the text a bit to explicitly reference the
                    visualization and explain the slight difference between
                    crossover and mutation use of the trade operation better

        -   ✅ gauss trade (direct enc)
        -   ✅ move single time alloc (direct encoding)
            -   🚧 feedback: describe in more detail (pseudo-code)

        -   ✅ gauss move single time alloc (direct enc)
        -   ✅ move sub event (direct enc)
            -   🚧 feedback: describe in more detail (pseudo-code)

    -   replacement
        -   ❌ full
        -   ❌ elite absolute
        -   ❌ elite relative

    -   termination
        -   ❌ generations
        -   ❌ objective value
        -   ❌ generations or objective value


<!-- Chapter 5 ------------------------------------------------------------- -->
## 5. Self-Parameterization
-   ❌ describe the proof of concept implemented for the eggholder function
    (which is a widely used benchmark for genetic algorithms)

<!-- Idea behind self-parameterization -->
-   ✅ The idea behind self-parameterization is twofold:
    1.  prevent premature convergence
    2.  reduce the need for parameter tuning, leading to more robust and
        versatile algorithms

    To tackle these issues, self-parameterization -- also called adaptive
    evolutionary techniques -- allow a genetic algorithm to dynamically adapt
    its behavior based on runtime metrics of the algorithm itself.
    The genetic algorithm framework used in this study includes the collection
    of a broad range of such runtime metrics which are exposed via its
    interfaces, for the actual algorithm implementation to use them.
    This allows the implementation of self-parameterization methods, which are
    also called "dynamics" in the context of this study (because they make
    the genetic algorithm's parameters dynamic).


<!-- Present all self-parameterizing methods I developed -->
-   ✅ list and describe all methods of self-parameterization
    -   describe small differences due to the encodings (direct/indirect)

    -   gauss_rand_event (used in direct + indirect encoding)
        -   if current success rate (calculated with PT1 lowpass filter) is
            lower than the given target success rate, the difference between
            those two values is calculated and added to the standard deviation
            used for the random number generator for events

        -   if the standard deviation value becomes larger than 1.5 times the
            emount of events in the problem instance, the standard deviation is
            reset to its default value

        -   also if a generation was successfull, meaning that the best solution
            in the current population has a lower cost thant the best solution
            in the previous generation, the standard deviation of the random
            event generator is also reset to its default value

        -   for this dynamic to take affect, it must be used in combination with
            mutation methods, that use a normally distributed number generator
            for generating random event indices.
            -   the direct encoding only has one mutation method, which works
                in this case, which is a variation of the "trade" mutation,
                which does not use a uniform distribution but a normal
                distribution for generating random numbers

            -   for the algorithm employing the indirect encoding this is
                similar, but with a variation on the swap mutation, where
                the variation is also in the distribution used for generating
                random events.

    -   gauss_rand_time (only used in direct encoding)
        -   this self-parameterization technique works exactly like the
            gauss_rand_event method, but instead it mutates the random
            number generator (and its standard deviation) which is used
            for generating random time indices

        -   again, this dynamic only takes effect when used in combination
            with mutation method, that use a random number generator which
            generates normally distributed numbers
            -   as generating time indices only occurs in the context of the
                direct encoding, only the corresponding algorithm implements
                such a mutation.
                The mutation is called "GaussMoveSingleTimeAlloc" and is
                a variation of the previously described "MoveSingleTimeAlloc"
                with the only difference being the random number generator used
                under the hood.

    -   inc_lin_rnk_sel_pressure (used in direct and indirect encoding)
        -   this dynamic sets the initial selection pressure of the linear
            rank selection to 1.0
        -   modification of the selection pressure is done in steps
        -   this dynamic accepts the following parameters:
            -   amount of generations to pass before another STEP is made
            -   step/increase in selection pressure value
            -   max selection pressure
            -   maximum amount of generations at max selection pressure
        -   the process of this dynamic then checks for how long (how many
            generations) the cost/fitness of the respective best individual
            in the population did not get better.
            If this amount of generations matches the first parameter, and
            increase in selection pressure is made by the amount given as the
            second parameter.
            If due to these increases the maximum desired selection pressure
            is reached, which is specified by the third parameter,
            or for an extended amount of generations, which is specified as
            the third parameter, no change in the best cost happened,
            the selection pressure is reset to 1.0

        -   because selection mechanisms are encoding agnostic, this dynamic
            can be employed in both, the direct and indirect encoded algorithms,
            as long as they use the linear rank selection method, because
            this dynamic only takes effect when using the linear rank selection.

    -   state_machine (used in direct and indirect encoding)
        -   the state machine dynamic involves different states of parameter
            sets, meaning that for each state change possibly multiple
            parameters of the algorithm are changed.
        -   the implementation used in this study comprises three states:
            broad, focus, finish
        -   after 200 generations in the broad state, the dynamic changes to
            the focus state, which is active for 1800 generations. After
            2000 generations in total, the dynamic switches to the finish
            state which is used for 3000 generations, after which the state
            machine dynamic returns to the broad state again.
        -   if the state machine goes four full circles, meaning that the
            algorithm did not find an optimal solution after 20000 generations,
            for the next 50 generations (in the broad state), the replacement
            strategy is changed to "full", where usually an elite of one
            individual is used
        -   the implementation of the state_machine dynamic differs slightly
            between the direct and indirect encoded algorithms.
            -   in case of the indirect encoded algorithm, the state machine
                uses two kinds of crossover methods: PMX and ordered.
                The direct encoded algorithms uses 1-trade crossover in
                all states
            -   similarly the indirect encoded algorithm uses two sorts
                of mutation methods, namely uniform swap and gauss swap.
                The direct encoded algorithm only uses the trade mutation.
            -   additionally the mutation rates differ depending on the
                encoding used. These fine differences are visualized in figure ...

    -   mut_rate_cos (used in direct and indirect encoding)
        -   this dynamic works regardless of the mutation method used, because
            it solely works by modifying the mutation rate, which is obivously
            used in all mutation methods.
        -   this dynamic modifies the mutation rate, so that the mutation rate
            follows a sine waveform.
        -   to parameterize this method, the following parameters need to be
            specified:
            1.default mutation rate (y-axis shift)
            2.amplitude (maximum change of the mutation rate in both directions)
            3.wavelength (in generations)
            4.optional min & max values (for a hard cutoff)

    -   VarMutRateTargetMeanSin (used in direct and indirect encoding)
        -   the goal of this dynamic is to reach a given mean objective value
            in the current populatoin
        -   this target mean objective value is not constant, but changes
            in a sine waveform
        -   to reach the mean objective target value, the dynamic modifies the
            mutation rate until the mean objective target value is met.
        -   for controling the amount of modification of the mutation rate,
            a PT2 control circuit is used.
        -   these are the parameter of this dynamic:
            -   average deviation from the current best (e.g. 1.10 for +10%)
            -   gain of the PT2 block (= amplification)
            -   amplitude of the deviation change (sine-function)
            -   wavelength (in generations)


<!-- Chapter 6 ------------------------------------------------------------- -->
## 6. Results
-   ✅ Introduction
    -   this chapter presents the results of executing the algorithms
        presented in this thesis multiple times, with different configurations
        and on both -- the htdd4 and hdtt5 -- problem instances.

    -   the results of these algorithm executions will be shown in different
        categories. The first category is "success rate", which is only
        interested in the fact if or if not a given algorithm with a certain
        configuration was able to solve the problem instance at hand
        (remember: solving means that the best individual of a population must
        have a objective value or cost of 0).
        The second metric of interest was then to also filter the data for
        successful runs only, and visualize how many generations the algorithms
        took with certain configurations to find a perfect timetable.
        The last metric which is considered part of the plain results is
        performance oriented and captures the number of generations the
        algorithms were able to calculate per second.
        All of results are visualized in diagrams which contain abbreviations
        for the algorithm, their configuration and -- if used -- the employed
        self-parameterization techniques.

    -   what is `alg_11` and `alg_12`
        -   the two algorithms presented in this thesis are called `alg_11`
            and `alg_12` in the diagrams which show the results.

        -   during the exploration phase of this surve, many algorithms have
            been developed until two approaches have been found, which
            can actually solve timetabling problem instances from the
            XHSTT archives. All of these algorithms were enumerated ascendingly,
            which results in the final genetic algorithms to be called
            `alg_11` and `alg_12`.
            `alg_11` is the genetic algorithm which employs the formerly
            described direct encoding, and `alg_12` consequently is the
            genetic algorithm which is based on the indirect encoding.

    -   explain naming of configurations and dynamics
        -   more complicated than the naming of the algorithms is surely the
            naming of their configuration and the self-parameterization methods
            they use.
            Despite of the complexity of their naming, using abbreviations
            for algorithm configurations and dynamics was crucial for being
            able to differentiate between these different algorithm parameters
            in the results.

        -   \ref{tab:ga-cfg-abbr} is a table of the configuration abbreviations
        -   \ref{tab:ga-dynamic-abbr} is a table of the
            dynamic/self-parameterization abbreviations


-   hdtt4
    -   alg_11 (direct encoding):
        -   ✅ static: no configuration has a 100% success rate
        -   ✅ dynamic: 100% success rate
        -   ✅ dynamic algorithm has higher runtimes (in generations) in 
            comparison to 3 (out of 5) of the tested static algorithms (these
            runtimes only take the success cases of the static algorithms into
            consideration)

    -   alg_12 (indirect encoding):
        -   ✅ static: multiple configurations have a 100% success rate
        -   ✅ dynamic: also multiple configs with 100% success rate
        -   ✅ self-parameterization causes slightly higher runtimes (in
            generations)

-   hdtt5
    -   alg_12 (indirect encoding):
        -   ✅ static: one config with 100% success rate
        -   ✅ dynamic: **no** config with 100% success rate
        -   ✅ self-parameterized algorithms performed worse than static ones


-   runtime/performance
    -   ✅ self-parameterization has no notable impact on performance
        (calculated generations per second)

    -  ✅ Name hardware which was used to run the algorithms for the captured runs

-   ✅ include plots for visualizing the results

-   ✅ GitHub Gax-Plots link - include github repo as citation as a source for
    raw data of the runs and source code of the plot generation (in R-Lang).
    URL: https://github.com/biwecka/gax-plots


<!-- Chapter 7 ------------------------------------------------------------- -->
## 7. Discussion
-   ✅ direct encoding
    -   ✅ the results clearly show that, independent of the used configuration,
        the algorithm using the direct encoding scheme cannot reliably solve
        the hdtt4 problem instance. In direct comparison, alg_12 with the
        indirect encoding achieves a 100% success rate and thereby a perfect
        reliability.

    -   ✅ figures 1 and 2 (direct_static_succ_median,
        direct_static_fail_median) show an average successful and unsuccessful
        run. thereby "average" actually means the median run of the respective
        algorithm and configuration in terms of the generations taken.

    -   ✅ these diagrams show, that without dynamic changes of the algorith
        parameters, there are no notable changes to the population metrics
        except for the obvious changes when better solutions are found.
        Other than that, especially when looking at the diversity value,
        the diversity stagnates or even decreses slightly over time.
        This means that if the algorithm might get stuck in a local maximum,
        without increasing its diversity, and thereby impacting the population
        metrics, the algorithm will not get out of this premature convergence
        and run until the generation limit terminates it with a non-optimal
        timetable solution.

    -   ✅ figure 3 (direct_dynamic_succ_median) on the other hand shows
        the median successful run of alg_11 with the state machine dynamic.
        The periodic changes of the employed self-parameterization technique
        are clearly visualized by this plot.
        As described in chapter "5.1.2 state machine", this dynamic cycles
        through three different states with a duration of 5000 generations
        per cycle. The cycles are clearly visible in the diagram, indicated
        by the recurring spikes of the worst objective value and diversity
        metric.

        ✅ This run also shows the biggest advantage of self-parameterization
        compared to the static variants of the algorithm.
        If the population stagnates for a too long, by not finding a overall
        better solution over many generations, the state machine dynamic
        interprets this as a form of premature convergence and resets the
        search progress of the genetic algorithm by disabling the elitist
        replacement strategy for a short period of 50 generations.
        This reset can be seen twice in in figure 3, at 25000 and 50000
        generations. By disabling the elite, the algorithm effectively
        removes all individuals from previous generations, which might lead
        to the best solution of the population getting slightly worse, but with
        the benefit of introducing more diversity into the population.
        This can be seen after the second "reset" at 50000 generations:
        the diversity level after the reset is slightly higher than all of
        the generations before.

-   ✅ indirect encoding
    -   ✅ the same contemplation of median successful and unsuccessful runs as
        shown for alg_11 can also be done with alg_12, which uses the indirect
        encoding strategy. Figure 5 show an execution with no
        self-parameterization which shows similar behavior to the direct
        encoding, except that the indirect encoding converges much faster
        and therefore needs a significant amount of less generations to find
        solutions. Additionally, figure 6 shows a unsuccessful execution of
        alg_12 also without dynamic. Be aware, that for visualizing a failed
        run, a different configuration has been used than in figure 5, because
        the configuraiton used in that figure always succeeded.
        The similarities between the direct and indirect encoding are:
        almost constant, slowly declining diversity value with no significant
        changes or spikes to any of the captured metrics.

        ✅ But when analyzed in detail, some notable differences can be found:
        First of all, the diversity value, albeit nearly constant, is
        significantly higher for the indirect encoding scheme, which
        signifies a broader exploration of the search space compared to the
        direct encoding.

        ✅ Secondly, in case of the direct encoding the best and median
        objective value are equal throughout the whole execution with the
        exception of short spikes in the median value. The mean value on the
        other hand is consistently worse.
        For the indirect encoding a whole different situation arises:
        The median an mean value are much closer to each other, with the
        median value seemingly always taking the closest whole number to
        the current mean value. Both are clearly set apart from the current
        best with big margin.
        This, and the relative position of the mean and median values to the
        respective best and worst objective value, which is sitting right
        in the middle between best and worst for the indirect encoding and
        skewed heavily towards the best objective value in case of the direct
        encoding method, shows that the direct encoding has a less diverse
        population resulting in premature convergence, which signifies
        in needing self-parameterization for getting perfect reliablility,
        whereas the indirect encoding has a more balanced population in
        terms of diversity, therefore does not suffer from premature convergence
        and even reaches a perfect reliability score for multiple configurations
        with and without self-parameterization.

        ✅ For completion, figure 7 shows the execution of alg_12 with
        the most elaborate self-parameterization technique of
        "5.1.6 VarMutRateTargetMeanSin". This figure impressively shows
        how the dynamic steering of this algorithms' parameters results in a
        constantly changing diversity of the population, which is especially
        visible in the last third of the plotted run, as the diversity
        increases slightly with the worst objective value rising in respondance
        and the algorithm then finding a solution.

-   ✅ comparison
    a question that inherently arises from the previous findings is:
    1. Why does the direct encoding tend to converge prematurely, thus needing
    self-parameterization to break out of local minima?
    2. And, what is the reason for the indirect encoding converging much faster,
    even without any dynamic parameterization?


    Regarding question 1: Although the specialized trade crossover and mutation
    methods are used for the direct encoding algorithm, which are implemented
    to resemble known hill climbing operations,
    and therefore are designed to not invalidate a chromosome but make
    sensible changes in the context of their meaning regarding the timetable
    they represent,
    the application of these operations might, despite correctly mutating
    the chromosome, in most cases lead to offspring with a very similar
    objective value as their parents. This behavior makes perfect sense, as
    those operations originate from a hill climbing algorithm, which likely
    had this as a design goal for its parameters.
    In the context of genetic algorithms those parameters also make perfect
    sense, but without self-parameterization the algorithm might get caught
    in a local maximum, which it cannot escape without adapting its parameters
    dynamically.
    Adding self-parameterization to the direct encoding algorithm therefore
    allows the observation of escaping those dead ends in form of local maxima,
    by effectively turning around, broadening up the search radius again
    to find a different path which possibly leads to an optimal solution
    This shows, that self-parameterization plays a crucial role in making
    alg_11 successfully solving the hdtt4 problem, as it would not be able
    to consistently do so without the use of self-parameterization.

    The indirect encoding (see question 2) on the other hand could not be
    improved by using self-parameterization techniques, which indicates
    a different cause than premature convergence for its unsuccessfulness
    in certain configurations. This cause is rooted in the fundamental
    differences between the direct and indirect encodings.
    Whereas the direct encoding, as the name implies, directly maps one
    genotype to one phenotype, the indirect encoding does not do that.
    For the indirect encoding, one genotype, which is only a scheduling order
    for the events of a problem instance, can be transformed into multiple
    phenotypes. That is the case because each timeslot can be schedule at
    various different timeslots, allowing a large amount of possibilities
    to schedule events to time slots for a single genotype. The employed
    heuristic unifies this process into a set of rules, to not only map the
    genotype to one of the possible phenotypes, but to a phenotype which
    has certain features which suit the algorithms search target. In the study,
    the heuristic for example completely outrules the existence of resource
    conflicts.

    This property of the heuristic makes the phenotypes each genotype
    is mapped to, very fit and leads to the observed superior, fast
    convergence of the indirect encoded algorithm, even though the indirect
    encoding has to explore a larger search space due to the permutation
    property of the chromosome.
    On the other hand, by mapping a genotype to only one possible phenotypes
    of a large set of phenotypes, skips over many possible solutions to a
    timetable problem. The distance between explored phenotypes and therefore
    the size of the set of phenotypes which are unexplored, explain why the
    indirect encoding can converge much faster than the direct encoding
    and also why it cannot be improved by self-parameterization.

    The reason for faster convergence is obvious, as the heuristic always
    ensures a very high quality of phenotypes and by skipping over large parts
    of the search space, the algorithm can explore the search space much faster,
    despite the search space being larger than in the direct encoding appraoch.
    As for the reason, why the indirect encoding could not be improved by
    self-parameterization, it also comes down to the heuristic. As previously
    mentioned, the failures of the indirect encoding can be explaind by
    the explored and skipped phenotypes of a genotype. If the skipped
    part of the search space is too large, meaning it contains a lot of
    potential solutions, it might contain many good or even perfect solutions.
    But as the self-parameterization techniques implemented in this study,
    as well as the heuristic algorithm, are not designed to modify the
    "focus"/focal length of the heuristic, none of the tested dynamic methods
    could improve the performance of alg_12.
    Therefore, by skipping large parts of the search
    space, likely only close to perfect solutions can be found, resulting
    in a similar situation as with premature convergence - the algorithm
    simply keeps running waiting to be terminated by the generation limit.


-   ✅ regarding research hypothesis:
    -   it depends on the used encoding
        -   direct encoding:
            -   ✅ needs self-parameterization to reliably succeed in finding
                solutions (100% success rate)

            -   ❌ runtime (in generations) slightly higher for dynamic
                algorithms (therefore they solve the problem more reliably;
                runtime is still not significantly higher than the runtime of
                the static algorithms)

        -   indirect encoding:
            -   ✅ due to the heuristic of the indirect encoding, the static
                algorithms perform already pretty good (multiple configurations
                with 100% success rate)

            -   ✅ the self-parameterized algorithm configurations did perform
                equally well and didn't improve the results notably (neither
                regarding the success rate, nor the runtime or performance)

        -   ✅ in case of **hdtt5** (harder than hdtt4), the static algorithm with
            indirect encoding is more reliable than the self-parameterized
            algorithms
            -   ✅ what about hdtt5 and why couldn't alg_11 solve it? the
                constant resets of the state machine dynamic worked for hdtt4
                as it may have a handable size for this. but as soon as the
                problem gets more complex (see hdtt5) this self-parameterization
                fails, because the search space might get too large for the
                algorithm to prematurely converge as fast as it does and being
                constantly set back by self-parameterization to get it out of
                local maxima.


<!-- Chapter 8 ------------------------------------------------------------- -->
## 8. Conclusion
-   ✅ adaptive evolutionary techniques in form of self-parameterizing methods
    don't universally improve any kind of GA

-   ✅ the effectiveness of self-parameterizing methods highly depends on the
    used encoding

-   ✅ the choice of self-parameterization method as well as its parameters are
    subject to the problem of parameter tuning just like the "normal" input
    parameters of a GA

    -   ✅ for the development of an adaptive evolution technique, which
        reduces the need for manual parameter tuning, it's likely necessary
        to analyze the behavior of the algorithm on a multitude of different
        problem instance, to then find a (probably very complex) method of
        dynamically change the GA's parameters


<!-- Chapter 9 ------------------------------------------------------------- -->
## 9. Future Work
-   ✅ extend algorithm/encoding ability to solve more problem instances from
    the XHSTT archives (including ones with advanced constraints)

-   ✅ design and develop more sophisticated self-parameterization techniques

-   ✅ the performance of the direct encoding could maybe be further improved
    by using the `BitsMxN` matrices instead of `Vec<Bits64>` in its genotype
    and phenotype.
    ->  these types were initially implemented to improve performance of the
        indirect encoding (because it's much heavier in computation). therefore
        they have not been included in the direct encoding yet.

-   ✅ test static direct encoding with more configurations

-   ✅ change "focal length" of the genotype-to-phenotype mapping of the
    indirect encoding and see how it changes the algorithm's behavior.
    maybe implemente self-parameterization techniques based on this.
