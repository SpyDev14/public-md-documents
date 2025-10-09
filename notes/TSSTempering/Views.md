BaseCompanyInfoPageView
- `all` FacilityImages `in order`
- `all` Products
- `all` Projects
- `calc` (int) лет на рынке

HomePageView(BaseCompanyInfoPageView)
AboutPageView(BaseCompanyInfoPageView)

ProductDetailView(BRMDetailView, !FormMixin)
- `all` Products `without` $this
- `form` FeedbackRequest

ProjectDetailView(BRMDetailView)
- `one` Project `who` next in order after $this

ProjectListView(PBLV)
- @filters by
	- `glass_area`
	- `completion_year`
	- `sity`

ArticleDetailView(BRMDetailView)
ArticleListView(PBLV)
- @filters by `category`
- `all` ArticleGroups