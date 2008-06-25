## Path Names

我的Blog(http://www.nomedojogo.com ，譯注：原作者的Blog)讀者們應該都知道我的**Custom Resource Name**外掛，但我想它應該就快要死亡了... :(

在Rails中你已經包含了**:as**選項在routes(一些我實現在外掛中保持相容性的東西)中，現在你也將擁有**:path_names**選項改變你**actions**的名字。
	
	map.resource :schools, :as => 'escolas', :path_names => { :new => 'nova' }

當然，我的外掛對於早期的Rails版本依然有效。