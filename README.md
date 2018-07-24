# Child-to-Parent-trigger-update
trigger Conaccupdate on Contact (after insert,after update ) {
   list<account> acclst = new list <account>();
    list<id> lid = new list<id>();
   
    for(contact c : trigger.new){
        lid.add(c.accountid);
       
        
    }
    acclst =[select id,(select id,email from contacts)from account where id IN :lid];
    for (account a :acclst){
        for(contact cts:trigger.new){
            a.Site = cts.Email;
            
        }
        
    }
    if(acclst.size()>0){update acclst;}

}
