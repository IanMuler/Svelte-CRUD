<script>
import {v4} from 'uuid'	

	let products=[
		
		{id: 0,
		name: "HP",
		description: "HP Pavilion",
		category: "laptops",
		imgurl: "https://ar-media.hptiendaenlinea.com/catalog/product/cache/b3b166914d87ce343d4dc5ec5117b502/2/2/22B04LA-1_T1621634041.png"},

		{id: 1,
		name: "Lenovo",
		description: "Lenovo PC",
		category: "laptops",
		imgurl: "https://static.kemikcdn.com/2019/01/887-1.jpg"}
	]
	
	let product={
		id: "",
		name: "",
		description: "",
		category: "",
		imgurl: "",
	}

	const noimg = "https://www.prolibro.cl/img/default/default-product-image.png"
	let onEdit = false;

	const resetForm = () => {
		product={
		id: "",
		name: "",
		description: "",
		category: "",
		imgurl: "",
	}
}
	const addProduct = () => {
		const newProduct = {
			...product,
			id: v4(),
		}
		console.log(newProduct)
		products = products.concat(newProduct)

		resetForm();
	}

	const updateProduct = () => {
		const updatedProduct = product;
		const productIndex = products.findIndex(p => p.id === product.id);

		products[productIndex] = updatedProduct;
		
		onEdit = false;
		resetForm();
	}

	const onSubmitHandler = (e) => {
		e.preventDefault();
		if(!onEdit){
		addProduct();
		} else {
		updateProduct();	
		}
	}

	const deleteProduct = id => {
		products = products.filter(product => product.id != id)
	}

	const editProduct = productEdit => {
		product = productEdit;
		onEdit = true;
	}

</script>

<main>

	<div class="container">
		<div class="row">
			<div class="col-md-6">

				{#each products as product}
					<div class="card mt-2 py-4">
						<div class="row">
							<div class="col-md-4">
								
								{#if product.imgurl}
								<img class="img-fluid" src={product.imgurl} alt="">
								{:else}
								<img class="img-fluid" src={noimg} alt="">
								{/if}

							</div>
							<div class="col-md-8">
								<div class="card-body">
									<h5>
										<strong>
											{product.name}
										</strong>
										<span>
											<small>{product.category}</small>
										</span>
									</h5>	
								</div>
								<p class="card-text">{product.description}</p>
								<button class="btn btn-danger" on:click={deleteProduct(product.id)}>
									Delete
								</button>
								<button class="btn btn-secondary" on:click={editProduct(product)}>
								
									Edit
								</button>
							</div>
						</div>
					</div>

				{/each}
			</div>
			<div class="col-md-5">
				<div class="card">
					<div class="card-body">
						<form on:submit={onSubmitHandler}>

							<div class="form-grop">
								<input bind:value={product.name} 
								type="text" 
								placeholder="Product name"
								class="form-control"/>
							</div>
							
							<div class="form-grop">
							<textarea bind:value={product.description} 
								id="product-description" 
								rows="3"
								class="form-control"/>
							</div>

							<div class="form-grop">
							<input bind:value={product.imgurl}
								type="url" 
								id="product-image-url" 
								placeholder="https://example.com"
								class="form-control"
								/>
							</div>
							
							<div class="form-grop">
								<select bind:value={product.category} id="category">
									<option value="" selected hidden>Select</option>
									<option value="laptops" >Laptops</option>
									<option value="perifericos">Periféricos</option>
									<option value="server">Servers</option>
								</select>
							</div>

							
							<button class="btn btn-secondary" type="submit">
								{#if onEdit}
								Edit product
								{:else}
								Save product
								{/if}
							</button>
						</form>
					</div>
				</div>
			</div>
		</div>
	</div>
</main>

<style>
	
</style>