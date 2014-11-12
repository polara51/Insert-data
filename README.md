
Insert-data
===========
/*
Inserting the data into the table(ie: weight.&amp;cc._ue_&amp;period &amp;cc is country code) and we are pulling the data from the 2 tables with the certain conditions(ie: UK_UE_dummy and nrcq.uk_hybrid_phx_ue here nrcq is library).
*/

Proc SQL;
insert into weight.&cc._ue_&period
(local_time, country_code, LEVELS, sl_id, surf_location, CATEGORY,
 demo_id, demo_value, demo_audience, demo_prc, validation_flag)
  SELECT a.local_time,
         a.country_code,
		 a.LEVELS,a.sl_id,
		 a.surf_location,
         b.CATEGORY,
		 b.demo_id,
 		 b.demo_value,
         a.demo_audience * b.demo_prc / 100 ,
		 b.demo_prc,b.validation_flag
  from UK_UE_dummy a,
       nrcq.uk_hybrid_phx_ue b    
  where a.Levels='Individual'
  and a.sl_id=4
  and a.demo_id=999
  and b.Levels='Individual'
  and b.sl_id=4
  and b.category='region'
  and b.local_time='01-Jul-2010'd;
quit;
