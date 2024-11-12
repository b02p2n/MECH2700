java c
MECH2700:  Computational  Engineering    Data  Analysis   (S2, 2024)
>  Seine  River  Contaminant  Transport
Assignment  2:  Convection-Diffusion  Modelling
AimThe aim of this assignment is to synthesise your understanding of parabolic and hyperbolic partial differential equations by developing a numerical scheme that models a physical process where both diffusion and convection are present. Your solutions are to be implemented in Python and formally documented in a report.
The ProblemDuring the Paris Olympic Games, multiple events were swum in the Seine River, shown in Figure 1. Despite a massive effort to clean up pollution in the river, there were still concerns for athlete safety, in part due to fresh contamination introduced during the games. The fresh contamination generally entered the river via inflows from one of the banks, and is then transported through a combination  of water flow and turbulent diffusion.  Health risks arise if the contaminant concentration exceeds  the safe threshold in the area of the river where athletes compete.

Figure  1:    Seine  river,   Paris   (France).      Taken  3  August   2013.      Source:
http://www.panoramio.com/photo/97777268. Author: Tommie Hansen.
With a limited number of assumptions, the distribution of the contaminant in the river can be modelled as a combination of diffusive and convective processes. The unforced, two-dimensional convection- diffusion equation when convection only occurs in the x-direction is,
in which c is the contaminant concentration (kg per cubic meter) and is a function of x, y and t, Dturb  = 0.2 m2 /s is a turbulent diffusion coefﬁcient, and v x is a x-velocity that is only dependent on y that is approximated as,
where V = 1.2 m/sand W1/2  = W/2.Consider a two-dimensional stretch of the Seine River, shown in Figure 2, which is W = 150 m wide and L = 750 m long. Initially, the river is free of contamination, c(x,y, 0) = 0. At t = 0, a steady stream of contamination with a peak concentration of c max  = 1 kg/m3 at they = 0 bank flows into the stretch of river with a half Gaussian distribution through the upstream boundary (x = 0). The standard deviation of the distribution is σ = 10 m. The contamination is free to leave the domain from downstream boundary atx = L, while there is no convection or diffusion through the river banks at y = 0 andy = W. To model this, the appropriate boundary conditions are a Diriclet condition on the inflow boundary, x = 0 m,
zero gradient at the downstream boundary, x = L m,

and zero flux on the side boundaries

Your task is to predict the propagation of contamination in the river and report on the concentration in the competition area of the river, 0.25W < y < 0.75W, in the time following contamination release.

Figure 2: Problem domain.The ﬁrst step in the numerical solution method is to discretise the domain along its length and width into a grid of equally spaced nodes where spacing between nodes is △x = △y = L/(nx - 1). nx is the number of nodes in the x-direction. The solution at a node located atx = i△x, y = j△yand t = m△t is denoted c .
Tasks
1. Determine the discrete form. of the convection-diffusion equation, at solution node (i, j). To do this, approximate the second order space derivatives with the central difference expression (using c values at time step m) e.g.,

the ﬁrst order space derivative with the upwind difference expression (using c values at time step m),

and the time derivative with a forward difference expression (equivalent to the forward Euler method for ODEs),
Present the discrete form. of the governing equation for an arbitrary interior node i,j.  Given the known errors in the ﬁnite difference approximations used (derived in an earlier section of MECH2700), what is the order of accuracy of the discrete governing equation in space and time?
2. Rearrange the discrete form. of the governing equation from Task 1 into an update equation for an
arbitrary internal node i, j (1 ≤ i ≤ nx  - 2, 1 ≤ j ≤ ny  - 2) of the form,
Next, determine the update equations for on the boundaries with i = 0, j = 0, j = ny  - 1 = jmax and i = nx  - 1 = imax. To do this, you will need to utilize the discr代 写MECH2700: Computational Engineering & Data Analysis (S2, 2024) Assignment 2: Convection-Diffusion ModellingPython
代做程序编程语言ete form. of the boundary conditions,

Note that the corner nodes do not influence the rest of the solution for the numerical approach we are taking.
3. Write a Python function to determine a stable timestep for a numerical solution to this problem for arbitrary grid spacing △x = △y. This is to betaken to the following conservative combination of the hyperbolic and parabolic timestep expressions:

Here, conservatively take the Courant-Friedrichs-Lewy number to be CFL = 0.45. Note that when you ﬁnd a solution with different resolution, the stable timestep will change.
4. Write a Python function to advance the solution for by one time step that takes the current array of c, t, △t and △x as inputs.  Utilize this function within a Python program that advances the solution in the entire domain from the initial condition at t  =  0 up to a maximum simulation time of t  = tmax. Record the full solution array every ≈200 s (to within △t).  Also record the concentration at the solution node nearest the edge of the competition zone at the end of the river segment x edge→ = (x, y) = (L, W/4) at every time step.
5. Use your numerical scheme to predict the contaminant concentration at x edge→ for t max   =  1000 seconds afer contaminant release.  Be sure to use a grid resolution that reasonably represents the contamination inflow proﬁle. Generate contour plots of the concentration distribution in the domain at 200 s, 400 s, 600 s, 800 s and 1000 safer release. Also create a graph of the concentration atx edge→ with time. Does the concentration exceed a threshold value of c safe  = 0.01 in this period? Suggest and justify how the boundary of the competition zone could be adjusted so that c(x,y, t) ≤ c safe for all time. To assess uncertainty in the turbulent diffusion coefﬁcient, how do your results change if the diffusion coefﬁcient is doubled to 0.4 m2 /s?
6. Repeat the above calculation for at least one other choice of grid spacing. Compare your results and comment on the grid-dependence of your numerical predictions. Given the trend in your solution with grid resolution, is the safe competition boundary you have established conservative (e.g. the errors in the numerical method lead to the boundary being further away from the contaminant source that it needs to be in reality)? Hints: Be reasonable, here.  If you try to run with a grid spacing of 1 mm you’re most likely going to have a bad time. Also, include something in your code that tells you how far into your simulation you are.
The Report
Document your work in a formal report that includes, but is not necessarily limited to, the following:
i. Introduction: A brief description of the problem you have been asked to solve;
ii. Methodology: The deﬁnition of your approach to solving this problem, including all working and relevant assumptions;
iii. Results: The appropriate presentation of results, which might include ﬁgures, graphs and tables;
iv. Concluding Remarks: A critical discussion of your approach to the problem and your ﬁndings. At a minimum this should include comment on the stability, convergence, accuracy and compu-tational efﬁciency of your scheme.
SubmissionWork individually or in groups of two for this assignment. Submit a single report for the group, de- tailing your analysis, code and results for Tasks 1 to 7. This report should be brief but well structured, so that the marker can easily interpret your results. Include your Python code and combine it all together into a single pdf ﬁle with a cover page that clearly tells us who you are.  Scanned, hand- written documents with appropriate cut-and-paste items are perfectly acceptable, but plots should be computer-generated.
For assessment of your work, the markers will be looking for answers to the following questions:
• Have you done what the tasks require? Note that your report should be well structured and tidy so that the marker can easily ﬁnd your answers.  Having your plots correctly titled and axes labeled is essential.
• Are your answers accurate?
• Is your code well-structured and clearly written, with suitable documentation comments?
• Does your code correspond to the results shown?

         
加QQ：99515681  WX：codinghelp  Email: 99515681@qq.com
