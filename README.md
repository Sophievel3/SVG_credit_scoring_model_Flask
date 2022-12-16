SVG_credit_scoring_model
            
            
                       I M P L E M E N T A T I O N   D'U N   M O D E L E   D E   S C O R E 
                            (Déploiement de la partie Flask dans le cloud avec Heroku).



Les URL de l'application Flask uploadée sur le cloud avec Heroku sont:
- https://svg-crsm-flask.herokuapp.com/  --> page initiale ("dashboard fait avec Flask").
- https://svg-crsm-flask.herokuapp.com/app/id  --> Liste des ID de tous les clients.
- https://svg-crsm-flask.herokuapp.com/app/client/?SK_ID_CURR=XXXXXX  --> Data du client choisi (ici: le client XXXXXX).**
- https://svg-crsm-flask.herokuapp.com/app/scoring_cust/?SK_ID_CURR=XXXXXX  --> Score du client choisi (ici: le client XXXXXX).**
- https://svg-crsm-flask.herokuapp.com/app/feat_imp_global  --> Features Importances Globales du modèle de score.
- https://svg-crsm-flask.herokuapp.com/app/feat_imp_local/?SK_ID_CURR=XXXXXX --> Features Importances Locales pour le client choisi (ici: le client XXXXXX).**

(**) Ne marchent pas sur le cloud à cause des problèmes de temps de calcul de plus de 30s avec Heroku.

---------------------------------------------------------------------------------------------------------


On retrouve ici tous les fichiers pour:
- Déployer la partie flask dans le cloud avec Heroku.

---------------------------------------------------------------------------------------------------------


INVENTAIRE DES FICHIERS PRESENTS:

1. Un dossier "templates"--> On y trouve le fichier "index.html", utilisé sur Flask pour afficher les résultats de LIME.

2. .gitattributes --> Document permettant d'utiliser Git LFS pour les fichiers des bases de données trop lourds.

3. **Base_complete.zip --> La base des données entière suite à tous ces traitements (train+test). (ie. Avec l'information de tous les clients, en format zip pour prendre moins de mémoire sur github). 

4. Base_test.zip --> Une partie de la base des données test initialement fournie (en format zip pour prendre moins de mémoire sur github)

5. Procfile.txt --> Document indiquant l'app à utiliser dans Heroku. 

6. **X_train_req_saved --> La base qui a servi pour entraîner et tester le modèle. (Celle ré-équilibrée avec SMOTE, en format zip pour prendre moins de mémoire sur github).

7. app.py --> Code Flask (tournant sur le cloud - Heroku). 

8. expl_pkl --> Le explainer résultant de l'analyse "LIME" de notre meilleur modèle.

9. global_pkl --> Les "Global Features Importances" de notre meilleur modèle.

10. model_pkl --> le meilleure modèle (LGBMClassifier), avec les meilleures hyperparamètres, entraîné et sauvegardé à l'aide du packaging "Pickle".

11. requirements.txt --> packagings et leur versions utilisés dans notre code flask.


(**) Ces deux bases là ne furent pas utilisées à cause des problème de mémoire sur Heroku.


---------------------------------------------------------------------------------------------------------

ATTENTION:

Compte tenue du fait que Heroku est devenu payant depuis le 28 novembre 2022 (500 euros le mois max selon 
le temps d'utilisation de leur serveur, mais on ne spécifie pas vraiment comment ils prennent en compte ce 
temps d'utilisation), le service gratuit étant limité à:

- une mémoire maximum utilisable du serveur de 512Mb et
- à l'exécution de taches qui prennent moins de 30s;



J'ai dû, dans la version du 'Dashboard cloud' (code: "P7_Sofia_Velasco_1_Dashboard_Cloud.py" et 
URL:https://sophievel2-svg-credit-p7-sofia-velasco-1-dashboard-cloud-gjc3bm.streamlit.app/):

- faire les tests sur une base de données bien réduite (que quelques lignes et uniquement de la base test, 
  afin d'éviter les erreurs de mémoire, erreur H12).
           --> Vous pouvez donc tester avec le ID: 100005 par exemple ou n'importe quel ID du fichier zippé 
               'base_test' disponible dans le repository 'SVG_credit_scoring_model_Flask'.


- lier le dashboard Streamlit, aux URL qui ne nécessitaient pas de chercher dans la base d'un client 
  spécifique. 
  En fait, même en réduisant énormément la base, cette tache prend plus de 30s à se faire sur leur serveur 
  et du coup elle génère un crash. Suite à en avoir discuté avec ma mentor, on a décidé donc de faire ainsi 
  dans le but de montrer que je sais bien lier un dashboard "Streamlit", à une app "Flask" mise dans le 
  cloud avec Heroku, comme il est demandé dans ce projet. Ce sachant bien sûr qur faisant tourner et l'app 
  Flask et le dashboard Streamlit en local, tout marche correctement et avec la base complète.
  (cf. Repository: 'SVG_credit_scoring_model_Dashboard_Local').
  

  Vous trouverez dans ce repository, tous les fichiers nécessaire et le code adapté pour la version uploadée
  dans le cloud avec Heroku. En gros, ce qui change de la version locale c'est que dans le fichier python 
  "app.py" on fait appel à la "Base_test" qui contient uniquement quelques lignes de la "base test" 
  initialement fournie.