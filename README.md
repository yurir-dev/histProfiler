# histProfiler

Very lightweight performance profiler based on inserting timestamps sampling in to the tested code.

{

  profiler::context ctx;
  
  loop {
  
	HistProfiler_Begin(ctx, “part1 of my code”)
	
	func(param1, param2);
	
	HistProfiler_End(ctx, “part1 of my code”)
	
  }
  
  or
  
  loop {
  
  	HistProfiled(ctx, "func1_profile", func, param1, param2)
  
  }
  
}


the result will be a histogram with sampled time frequencies, for example, tested code took 100ns 123 times and 200ns 20 times, and so on. 

if compilation flag ENABLE_HIST_PROFILER is set, it will collect data, if not these commands will be empty (void())

It accumulates these samples in histograms where X-axis represent measured time in specified units and Y-axis represent number of times it took the code to run.

The amount of memory  used by the profiler is constant and the CPU usage is minimal – a lookup in a std::unordered_map and some arithmetics.
So it can collect data for a very long time without affecting program performance.

The accumulated data can be dumped to std::out or a text file. 

To visualize the data, 1) copy&paste it into excel,  2) select all. 2) insert your favorite chart. See example in the docs/charts.png.

---------

profilerApi.h contains the interface

profiler.h, histogram.h contain all the implementation.

main.cpp and tests/test_*.cpp – contain several examples.

