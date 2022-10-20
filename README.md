# foreach_async_SR

in hpx::main():

define four policies: seq_pol, par_pol,par_sr_pol,par_task_sr_pol:

1.using following sentences to calculate the time: (using decltype) 
    
        double SEQ = test<decltype(seq_pol), std::false_type>(seq_pol, 10, n, std::false_type{});
        double PAR = test<decltype(par_pol), std::false_type>(par_pol, 10, n, std::false_type{});
        double Par_SR = test<decltype(par_sr_pol), std::false_type>(par_sr_pol, 10, n, std::false_type{});
        double Par_Task_SR = test<decltype(par_task_sr_pol), std::true_type>(par_task_sr_pol, 10, n, std::true_type{});

  --->>  when threads number = 32:  the results of par_sr_pol,par_task_sr_pol show up&down trend.
  plots: check 
    
2.using following sentences to calculate the time: (dont use decltype) 

         double SEQ = test(seq_pol, 10, n, std::false_type{});
         double PAR = test(par_pol, 10, n, std::false_type{});
         double Par_SR = test(par_sr_pol, 10, n, std::false_type{});
         double Par_Task_SR = test(par_task_sr_pol, 10, n, std::true_type{});
         
  --->>  when threads number = 32:  the results of par_sr_pol,par_task_sr_pol *didnt show up&down trend .       

### In sum, when threads num >=32, par_sr_pol(i.e, par.on(exec) ),par_task_sr_pol (i.e, par(task).on(exec)) shows bad perfromance; else(threads num <32), par.on(exec), par(task).on(exec) shows better performance than par policy.
        
