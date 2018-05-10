# best-repo-2
sf module challange

adding some custom content from my favorite text editor

/**********************************************************************************************************************/
/*  Major Board Info -- Cleaning up and Builing on SQL Query for SuperC                                               */
/*  Migrate, and integrate w                                                                                          */
/*                                                                                                                    */
/*  Date Created:  May 03, 2018                                                                                       */
/*  Last Modified: May 04 2018                                                                                        */
/**********************************************************************************************************************/


/*Create VIEW [Analytics\tableau].Major_Board_Info As*/
  WITH

  preBOD As (
  SELECT
        c.Id as Contact_Id,
        CASE WHEN (vp.AQB__Volunteer_Position__c = 'Board of Directors' and vp.AQB__ActiveFlag__c = 'true') THEN '2'
             WHEN (vp.AQB__Volunteer_Position__c = 'Board of Directors' and vp.AQB__ActiveFlag__c = 'false') THEN '1'
        ELSE 0
        END Board_of_Directors,

        CASE WHEN (vp.AQB__Volunteer_Position__c = 'Board of Regents' and vp.AQB__ActiveFlag__c = 'true') THEN '2'
             WHEN (vp.AQB__Volunteer_Position__c = 'Board of Regents' and vp.AQB__ActiveFlag__c = 'false') THEN '1'
        ELSE 0
        END Board_of_Regents,

        CASE WHEN (vp.AQB__Volunteer_Position__c = 'Board of Governors' and vp.AQB__ActiveFlag__c = 'true') THEN '2'
             WHEN (vp.AQB__Volunteer_Position__c = 'Board of Governors' and vp.AQB__ActiveFlag__c = 'false') THEN '1'
        ELSE 0
        END Board_of_Governors

     FROM [salesforce backups].dbo.Contact c
       INNER JOIN [salesforce backups].dbo.AQB__VolunteerPosition__c AS vp ON vp.AQB__Contact__c = c.Id
     /*WHERE vp.AQB__Volunteer_Position__c IN ('Board of Directors', 'Board of Regents', 'Board of Governors')*/
     where /*c.Id = '00336000015rHC2AAM'
       And*/ vp.AQB__Volunteer_Position__c in ('Board of Directors', 'Board of Regents', 'Board of Governors')
     Group by c.Id, vp.AQB__Volunteer_Position__c, vp.AQB__ActiveFlag__c

  ) Select /*Distinct*/
  ...
