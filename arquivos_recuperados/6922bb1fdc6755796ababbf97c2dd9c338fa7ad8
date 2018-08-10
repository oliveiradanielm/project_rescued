# encoding: utf-8
class <%= controller_class_name %>Controller < ApplicationController
  before_action :set_<%= singular_table_name %>, only: [:show, :edit, :update, :destroy]
  add_breadcrumb "<%= plural_table_name.capitalize %>", :<%= plural_table_name %>_path
  add_breadcrumb "Detalhar", :<%= singular_table_name %>_path, only: [:show]
  add_breadcrumb "Incluir ", :new_<%= singular_table_name %>_path, only: [:new, :create]
  add_breadcrumb "Editar", :edit_<%= singular_table_name %>_path, only: [:edit, :update]

  respond_to :html
  def index
    @<%= plural_table_name %> = <%= orm_class.all(class_name) %>
    @<%= plural_table_name %>_grid = initialize_grid(<%= orm_class.all(class_name) %>,
      order: :created_at,
      order_direction: 'asc',
      name: 'u1',
      csv_file_name: "<%= plural_table_name %>_#{Time.now.strftime('%d%m%y%H%M%S')}")
  end

  def show

  end

  def new
    @<%= singular_table_name %> = <%= orm_class.build(class_name) %>
  end

  def edit
  end

  def create
    @<%= singular_table_name %> = <%= orm_class.build(class_name, "#{singular_table_name}_params") %>

    respond_to do |format|
      if @<%= orm_instance.save %>
        format.html { redirect_to <%= plural_table_name %>_url, notice: I18n.t("messages.cadastro_sucesso", :model => "<%= singular_table_name.capitalize %>") }
        format.json { render :show, status: :created, location: @<%= singular_table_name %> }
      else
        format.html { render :new }
        format.json { render json: @<%= orm_instance.errors %>, status: :unprocessable_entity }
      end
    end
  end

  def update
    if @<%= orm_instance.update("#{singular_table_name}_params") %>
        redirect_to <%= plural_table_name %>_url, notice: t('messages.atualizado_sucesso', :model => "<%= singular_table_name.capitalize %>")
    else
      render :edit
    end
  end

  def destroy
    @<%= orm_instance.destroy %>
    redirect_to <%= index_helper %>_url, notice: t('messages.delecao_sucesso', :model => "<%= singular_table_name.capitalize %>")
  end

  private
    # Use callbacks to share common setup or constraints between actions.
    def set_<%= singular_table_name %>
      @<%= singular_table_name %> = <%= orm_class.find(class_name, "params[:id]") %>
    end

    # Only allow a trusted parameter "white list" through.
    def <%= "#{singular_table_name}_params" %>
      <%- if attributes_names.empty? -%>
      params[:<%= singular_table_name %>]
      <%- else -%>
      params.require(:<%= singular_table_name %>).permit(<%= attributes_names.map { |name| ":#{name}" }.join(', ') %>)
      <%- end -%>
    end
end
